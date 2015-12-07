---
layout: post
title: Android http开发（－） 下载web页面
category: android
tags: [Http]
keywords: android,http
description: 
---

    Android中HTTP协议的开发还是比较重要的，熟练的掌握HTTP开发，有助于开发效率，给用户一个更加优秀的APP产品。Android 中使用HTTP协议开发可以使用java自带的API－HttpURLConnection，也可以使用Apache HttpClient。下面就以这两种方式分别实现对一个web页面的下载。
    
###         (-)HttpURLConnection 实现一个页面的下载。

    /**
	 * TODO
	 * yumo 利用java的HttpConnectionURL 访问一个网站，并获取它的网站数据。
	 * @param url 要下载web页面的网址，比如Http://www.baidu.com
	 * @return
	 * int
	 * 2015-1-1
	 */
	private int getByJavaHttp(String webSite)
	{
		int statusCode = -1;
		try {
			//见一个一个URL
			URL url = new URL(webSite);
			//访问web页面
			HttpURLConnection httpConnection = (HttpURLConnection) url.openConnection();
			//获取返回的状态吗。
			statusCode = httpConnection.getResponseCode();
			//获取下砸的web页面数据。
			InputStream inputStream = new BufferedInputStream(httpConnection.getInputStream());
			Reader reader = new InputStreamReader(inputStream);
			String strResult = "";
			int c;
			while( (c = reader.read()) != -1)
			{
				strResult += String.valueOf((char)c);
			}
			Log.d(TAG,"getByJavaHttp: " + strResult);
		} catch (MalformedURLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return statusCode ;
	}
	
### （二） 通过ApacheHttpClient 实现一个web页面的下载

    /**
	 * TODO
	 * yumo 打印网站的数据 利用Apache httpClient
	 * @param url 网站名称 比如http://www.baidu.com
	 * @return
	 * int 返回请求结果
	 * 2015-1-1
	 */
	private int getByApacheHttp(String url) 
	{
		int statusCode = -1;
		//建立一个网络请求
		HttpGet httpRequest = new HttpGet(url);
		HttpClient httpClient = new DefaultHttpClient();
		try {
			//执行请求网络。
			HttpResponse httpResponse = httpClient.execute(httpRequest);
			//获取网络状态吗
			statusCode = httpResponse.getStatusLine().getStatusCode(); 
			if( statusCode == HttpStatus.SC_OK)
			{
				//如果成功获取数据则打印日志。
				String strResult = EntityUtils.toString(httpResponse.getEntity());
				Log.d(TAG, "getByAndroidHttp:"+strResult);
			}else
			{
				Log.d(TAG,"getByAndroidHttp errorCode :"+ statusCode);
			}
		} catch (ClientProtocolException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return statusCode;
	}





