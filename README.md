# Dockerized-httpserver
#httpserver has been written with Java (below codes).
#Author (TAYEBI) is a researcher in Parma university. In 2018 he has proposed evaluation of a dockerized web-application.
#compare the results with another virtual environmens (Vbox-NEMO).
#NEMO is a java virtual network emulator (has been proposed by prof Luca VELTRI) which its codes exist in github.
import java.math.BigInteger;

import java.io.IOException;
import java.io.OutputStream;

import java.net.ServerSocket;
import java.net.Socket;
import java.util.Date;
import java.util.HashMap;

import org.zoolu.util.Clock;
import org.zoolu.util.DateFormat;
import org.zoolu.util.Flags;
import org.zoolu.util.LoggerLevel;
import org.zoolu.util.Random;
import org.zoolu.util.SystemUtils;

import it.unipr.netsec.nemo.http.HttpRequest;
import it.unipr.netsec.nemo.http.HttpRequestHandle;
import it.unipr.netsec.nemo.http.HttpResponse;
import it.unipr.netsec.nemo.http.HttpServerListener;


/** Very simple HTTP server based on NEMO HTTP implementation.
 */
public class HttpServer {
	
	
	
	/** Verbose mode */
	public static boolean VERBOSE=false;
//	private static PrintWriter out = null;

	/** Logs a message. */
	private void log(String str) {
		SystemUtils.log(LoggerLevel.INFO,getClass(),str);
	}

	/** Server socket */
	ServerSocket server_socket;
	
	/** Server listener */
	HttpServerListener listener;
	
	
	/** Creates a new HTTP server.
	 * @param tcp TCP layer
	 * @param server_port server port
	 * @param listener server listener that handles HTTP requests
	 * @throws IOException */
	public HttpServer(int server_port, HttpServerListener listener) throws IOException {
		server_socket=new ServerSocket(server_port);
		this.listener=listener;
		
	//	if (this.out == null) {
	//		try {
	//			this.out = new PrintWriter("x.txt");
	//		}
	//		catch (FileNotFoundException e) {
	//			e.printStackTrace();
	//		}
	//	}
		
		serve();
	}
	
	
	/** Starts the server.
	 * @throws IOException */
	private void serve() throws IOException {
		if (VERBOSE) log("serve(): listening on port "+server_socket.getLocalPort()); 
		while (true) {
			final Socket socket=server_socket.accept();
			if (VERBOSE) log("serve(): new TCP connection"); 
			new Thread(new Runnable() {
				@Override
				public void run() {
					try {
						serve(socket);
					}
					catch (IOException e) {
						e.printStackTrace();
					}		
				}				
			}).start();
		}
	}

	
	//public static double getRandomDouble() { 
	
        // create instance of Random class 
      
//} 
	
	
	/** Handles a connection.
	 * @param socket the new TCP connection
	 * @throws IOException */
	private void serve(Socket socket) throws IOException {
		// request
		HttpRequest req=HttpRequest.parseHttpRequest(socket.getInputStream());
		if (VERBOSE) log("Request: "+req+"-----End-of-message-----");
		HttpRequestHandle request_handle=new HttpRequestHandle(req.getMethod(),req.getRequestURL());
		listener.onHttpRequest(request_handle);	
		// response
		HashMap<String,String> header_fields=new HashMap<String,String>();
		header_fields.put("Date",DateFormat.formatEEEddMMMyyyyhhmmss(new Date(Clock.getDefaultClock().currentTimeMillis())));
		header_fields.put("Server","Nemo Httpd");
		byte[] resource_value=request_handle.getResourceValue();
		String content_type=request_handle.getContentType();
		if (resource_value!=null && content_type!=null) header_fields.put("Content-Type",content_type);
		HttpResponse resp=new HttpResponse(request_handle.getResponseCode(),header_fields,resource_value);
		if (VERBOSE) log("Response: "+resp+"-----End-of-message-----");
		OutputStream os=socket.getOutputStream();
		os.write(resp.getBytes());
		os.flush();
		socket.close();		
	}

	
	/** Stops the server. */
	public void close() {
		try {
			server_socket.close();
		}
		catch (IOException e) {
			e.printStackTrace();
		}
	}
	


	/** Starts a HTTP server. 
	 * @throws IOException */
	public static void main(String[] args) throws IOException {
		
		
		Flags flags=new Flags(args);
		boolean help=flags.getBoolean("-h","prints this message");
		int port=flags.getInteger(null,"<port>",9090,"server port");
		
	
		   
         
	
		if (help) {
			System.out.println(flags.toUsageString("-jar nemohttpd.jar"));
			return;
		}
		


		new Thread(new Runnable() {
	         @Override
	         public void run() {
	          	        	 
	        	  Random rand = new Random(); 
	        	    
	              BigInteger b1 = new BigInteger("1"); // Or BigInteger.ONE 
	           //   BigInteger b2 = new BigInteger("1");
	            //  BigInteger b3 = new BigInteger("1");
	           //   BigInteger b4 = new BigInteger("1");
	              BigInteger b ;
	              
	              for(int i=1;i<=20;i++) {
	                  //	System.out.print("Process Counter :  "+b+" ");
	                   	
	                   	 try {
	            				Thread.sleep(500);
	            			} catch (InterruptedException e) {
	            				// TODO Auto-generated catch block
	            				e.printStackTrace();
	            			} // Wait 10 seconds
	              	 
	           
	              // Generate random integers in range 0 to 999 
	              int rand_int1 = rand.nextInt(1000000000); 
	              int rand_int2 = rand.nextInt(1000000000); 
	              int rand_int3 = rand.nextInt(1000000000); 
	              int rand_int4 = rand.nextInt(1000000000);
	              int rand_int5 = rand.nextInt(1000); 
	              int rand_int6 = rand.nextInt(1000);
	              int rand_int7 = rand.nextInt(1000); 
	              int rand_int8 = rand.nextInt(1000);
	              int rand_int9 = rand.nextInt(1000); 
	              int rand_int10 = rand.nextInt(1000);
	              
	                
	              b1 = b1.multiply(BigInteger.valueOf(rand_int1));
	              
	              
	         //     b2= b2.multiply(BigInteger.valueOf(rand_int2));
	         //     b3 = b3.multiply(BigInteger.valueOf(rand_int3));
	         //     b4= b4.multiply(BigInteger.valueOf(rand_int4));
	              
	              
	              
	              b = b1.pow(rand_int5); 
	            
	       // 
	              System.out.println("[Power: "+b); 
	           //        x=x+10;     
	            //   Print random integers 
	            // System.out.println("Random Integers: "+rand_int1); 
	          //   System.out.println("Random Integers: "+rand_int2); 
	           //  System.out.println("Random Integers: "+rand_int3); 
	           //  System.out.println("Random Integers: "+rand_int4); 
	          //   System.out.println("Random Integers: "+rand_int5); 
	          //   System.out.println("Random Integers: "+rand_int6); 
	         //    System.out.println("Random Integers: "+rand_int7); 
	          //   System.out.println("Random Integers: "+rand_int8); 
	          //   System.out.println("Random Integers: "+rand_int9); 
	           //  System.out.println("Random Integers: "+rand_int10); 
	             
	              // Generate Random doubles 
	              double rand_dub1 = rand.nextDouble(); 
	              double rand_dub2 = rand.nextDouble(); 
	              double rand_dub3 = rand.nextDouble(); 
	              double rand_dub4 = rand.nextDouble(); 
	              double rand_dub5 = rand.nextDouble(); 
	              double rand_dub6 = rand.nextDouble(); 
	              double rand_dub7 = rand.nextDouble(); 
	              double rand_dub8 = rand.nextDouble(); 
	              double rand_dub9 = rand.nextDouble(); 
	              double rand_dub10 = rand.nextDouble(); 
	            //  	x=x+10;  
	              // Print random doubles 
	            //  System.out.println("Random Doubles: "+rand_dub1); 
	           //   System.out.println("Random Doubles: "+rand_dub2);
	           //   System.out.println("Random Doubles: "+rand_dub3); 
	           //   System.out.println("Random Doubles: "+rand_dub4);
	           //   System.out.println("Random Doubles: "+rand_dub5); 
	           //   System.out.println("Random Doubles: "+rand_dub6);
	           //   System.out.println("Random Doubles: "+rand_dub7); 
	           //   System.out.println("Random Doubles: "+rand_dub8);
	            //  System.out.println("Random Doubles: "+rand_dub9); 
	              //System.out.println("Random Doubles: "+rand_dub10);
	             
	              
	            //  out.println(Double.toString(rand_dub2));
	          } 
	        	 
	         }
	         
	         
	         
	         
	}).start();

		
		
       
     
		
		new HttpServer(port,new HttpServerListener() {
			
			@Override
			public void onHttpRequest(HttpRequestHandle req_handle) {
						
				//System.out.println(getRandomDouble());
				
			//	while (1>0) {
				if (req_handle.getMethod().equals("GET") && req_handle.getRequestURL().equals("/")) {
					
					//String random = Double.toString(getRandomDouble());
					//System.out.println(getRandomDouble());
			//		PrintWriter out = new PrintWriter("filename.txt");
					
				//	new Thread(new Runnable() {
				//		@Override
				//		public void run() {
				//			getRandomDouble();
				//		}
				//	}).start();
					
					Random rand = new Random();
					String rand_dub2 = Double.toString(rand.nextDouble()); 
					

					
					
					String resource_value="<html>\r\n" + 
							"<body>\r\n" + 
							"<h1>Hello World!</h1>\r\n" +
						//	"<h1>wwwwwwwwww!</h1>"+
					
							"<p>Random value: "+rand_dub2+"</p>\r\n" +
						//	"do{<p>getRandomDouble()} while (1>0)"+
						
							"</body>\r\n" + 
							"</html>";
					
					
					req_handle.setContentType("text/html");
					req_handle.setResourceValue(resource_value.getBytes());
					req_handle.setResponseCode(200);
					//}
				
					
				}
				
			}	
			
		});
		
	}
	

}
