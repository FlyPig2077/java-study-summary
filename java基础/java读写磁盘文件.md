**参考：**
https://blog.csdn.net/qq_30141957/article/details/80049128

https://blog.csdn.net/liuhenghui5201/article/details/8279557

https://blog.csdn.net/lykangjia/article/details/70159619

https://blog.csdn.net/Chianz632/article/details/79946851

https://www.runoob.com/java/java-files-io.html

https://www.cnblogs.com/lianghui66/p/3303546.html

### 一、java的IO流

java中的IO流可分为字节流和字符流。其中有4个文件流，4个缓冲流，2个转换流，2个打印流，2个序列化流，2个数据流。

#### 文件流

```
FileInputStream            //字节输入流
FileOutPutStream           //字节输出流
FileReader                 //字符输入流
FileWriter                 //字符输出流
```

#### 缓冲流

```
BufferedInputStream        //字节输入缓冲流
BufferedOutputStream       //字节输出缓冲流
BufferedReader             //字符输入缓冲流
BufferedWriter             //字符输出缓冲流
```

**BufferedReader** 由Reader类扩展而来，提供通用的缓冲方式文本读取，readLine读取一个文本行，

从字符输入流中读取文本，缓冲各个字符，从而提供字符、数组和行的高效读取。

**BufferedWriter** 由Writer 类扩展而来，提供通用的缓冲方式文本写入， newLine使用平台自己的行分隔符，

将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组和字符串的高效写入。

#### 序列化流

```
ObjectInputStream          
ObjectOutputStream
```

#### 转换流（字符流）将字节流转换为字符流

```
InputStreamReader
OutputStreamWriter
```

#### 数据流

```
DataInputStream
DataOutputStream
```

#### 打印流

```
PrintWriter
PrintStream
```

### 二、使用示例

#### 1、使用FileWriter和BufferedWriter写入字符串到磁盘中

```
	/**
	 * 写入磁盘，并保存在磁盘中
	 */
	public static void writeToFile() {
		String content = "测试写入文件";
		File file = new File("H:\\workplaces\\eclipse_programs\\DataStructures\\testWrite.txt");
		try {
			//创建字符输出流类对象和已存在的文件相关联;文件不存在的话，并创建;true表示从结尾续写，false表示覆盖重写
			FileWriter fw = new FileWriter(file,false);
			BufferedWriter bw = new BufferedWriter(fw);
			//写入字符串内容
			bw.write(content);
			//关闭流
			bw.close();
			fw.close();
			System.out.println("测试写入成功");
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
```

#### 2、使用FileInputStream、InputStreamReader、BufferedReader从磁盘文件中读取内容

```
	/**
	 * 从磁盘文件中读取内容
	 * @return
	 * @throws IOException 
	 */
	public static void readFromFile(File file) {
		if(file.isFile() && file.exists()) {
			try {
				//FileInputStream用于从文件读取数据,读取文件成字节流
				FileInputStream fs = new FileInputStream(file);
				//使用InputStream从文件里读取数据，将字节流转换为字符流.
				InputStreamReader isr = new InputStreamReader(fs);
				//从字符输入流中读取文本，缓冲各个字符
				BufferedReader br = new BufferedReader(isr);
				
				StringBuffer sb = new StringBuffer();
				String text = null;
				while((text = br.readLine()) != null) {
					//将读取到的文本存入stringbuffer中
					sb.append(text);
				}
				System.out.println("读取结果：" + sb.toString());
				
			} catch (Exception e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}
```

#### 3、使用FileOutputStream 和 OutputStreamWriter写入文件

```
	/**
	 * 使用FileOutputStream 和 OutputStreamWriter写入文件
	 */
	public static void writeToFile2() {
		String content = "测试写入文件2";
		File file = new File("H:\\workplaces\\eclipse_programs\\DataStructures\\testWrite2.txt");
		try {
			//字节输入流
			FileOutputStream fs = new FileOutputStream(file);
			//将字节流转换为字符流
			OutputStreamWriter os = new OutputStreamWriter(fs);
			os.write(content);
			os.close();
			fs.close();
			System.out.println("成功写入文件2");
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
```

