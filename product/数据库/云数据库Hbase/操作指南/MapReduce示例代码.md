##  Map类
```
import java.io.IOException;
import java.util.Map;
import java.util.NavigableMap;

import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.io.ImmutableBytesWritable;
import org.apache.hadoop.hbase.mapreduce.TableMapper;
import org.apache.hadoop.hbase.util.Bytes;
import org.apache.hadoop.io.Text;

public class Mapper extends TableMapper<Text, Text>{
	@Override
	  protected void map(ImmutableBytesWritable rowkey, Result columns, Context context)
	      throws IOException, InterruptedException{
	    NavigableMap<byte[], byte[]> map = columns.getFamilyMap(Bytes.toBytes("retcode"));
	    for (Map.Entry<byte[], byte[]> ent : map.entrySet()) {
	        String retcode=Bytes.toString(ent.getKey());
	        String value = Bytes.toString(ent.getValue());
					
	        Text retkey = new Text(retcode);
	        Text retvalue = new Text(value);
	        context.write(retkey, retvalue);
	      }
	  }
}
```

##  Reduce类
```
import java.io.IOException;
import org.apache.hadoop.hbase.io.ImmutableBytesWritable;
import org.apache.hadoop.hbase.mapreduce.TableReducer;
import org.apache.hadoop.io.Text;

public class Reduce extends TableReducer<Text, Text, ImmutableBytesWritable> {
	 @Override
	  protected void cleanup(Context context) throws IOException, InterruptedException {

	  }

	  @Override
	  protected void setup(Context context) throws IOException, InterruptedException {

	    super.setup(context);
	  }

	  @Override
	  public void reduce(Text key, Iterable<Text> values, Context context) throws IOException, InterruptedException {

	    long size = 0;
	    String rowkey = key.toString();
	    System.out.println(rowkey);
	    for(Text t:values){
	    	System.out.println(t.toString());
	    }
	  }
}
```
##  提交任务
```
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.client.Scan;
import org.apache.hadoop.hbase.mapreduce.TableMapReduceUtil;
import org.apache.hadoop.hbase.util.Bytes;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.output.NullOutputFormat;

public class MR {

	public static void main(String[] args) throws Exception{
		Job job =Job.getInstance();
		Configuration conf=job.getConfiguration();
		// 填写zookeeper地址，多个地址用英文逗号隔开
		conf.set("hbase.zookeeper.quorum", "10.66.133.178:2181");
		//必填：填写云平台Hbase实例ID
	    conf.set("yarn.chbase.tencent.instanceid", "chb-lpvsvdlr");
		job.setJobName("testjob");
		
	    String tableName = "monitordata_201603";
	    Scan scan = new Scan();
	    scan.setStartRow(Bytes.toBytes("0800:00_00000000"));
	    scan.setCaching(500);
	    scan.setCacheBlocks(false);
	    job.setJarByClass(MR.class);
	    job.setReducerClass(Reduce.class);
	    job.setOutputFormatClass(NullOutputFormat.class);
	    job.setNumReduceTasks(5);
	    //如果要使用第三方jar包，可使用该工具类上传
	    //job.addFileToClassPath(JobHelper.addJarToDistributedCache(GenericObjectPoolConfig.class, conf));
	    
	    TableMapReduceUtil.initTableMapperJob(tableName, scan, Mapper.class, Text.class, Text.class, job);
	    
	    boolean b = job.waitForCompletion(true);
	    if (!b) {
	      throw new Exception("error with job!");
	    }
	}
```

##  工具类（如果需要使用第三方jar包）

```
import java.io.IOException;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.conf.Configuration;
import java.io.File;

public class JobHelper {

	public JobHelper() {

	}

	public static Path addJarToDistributedCache(Class classToAdd, Configuration conf) throws IOException {

		// Retrieve jar file for class2Add
		String jar = classToAdd.getProtectionDomain().getCodeSource().getLocation().getPath();

		File jarFile = new File(jar);

		// Declare new HDFS location
		Path hdfsJar = new Path("/tmp/hadoop/userlib/" + jarFile.getName());

		// Mount HDFS
		FileSystem hdfs = FileSystem.get(conf);

		// Copy (override) jar file to HDFS
		hdfs.copyFromLocalFile(false, true, new Path(jar), hdfsJar);
		hdfs.close();
		return hdfsJar;
	}
}

```