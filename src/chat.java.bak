import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.StringReader;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;

import javax.swing.JFrame;


public class chat {
	public static void  main(String[] args) {
		
		
		
		
		
		try {
			DatagramSocket sendSocket=new DatagramSocket();
			DatagramSocket receSocket=new DatagramSocket(10002);
			BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(System.in));
			String resource = null;
			while(true){
				try {
					resource = bufferedReader.readLine();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				new Thread(new Send(sendSocket,resource)).start();
				new Thread(new Receive(receSocket)).start();
			
			}
		} catch (SocketException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
	
	
	
}

class Send implements Runnable{
	private DatagramSocket sendSocket;
	String resource ;
	public Send(DatagramSocket sendSocket,String resource){
		this.sendSocket=sendSocket;
		this.resource=resource;
	}
	@Override
	public void run(){
		try {
			
			BufferedReader sendMassage=new BufferedReader(new StringReader(resource));
			while (true){
				String sendString=sendMassage.readLine();
				if(sendString==null){
					sendString="你的发送信息为空";
				}
				else{
					byte[] sendByte=sendString.getBytes();
					DatagramPacket sendPacket=new DatagramPacket(sendByte, sendByte.length,InetAddress.getByName("Nelson"),10002);
					sendSocket.send(sendPacket);
				}
				if(sendString.equals("over"))
					break;
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
		
	}

	
}


class Receive implements Runnable{
	private DatagramSocket receiveSocket;
	public Receive(DatagramSocket receiveSocket) {
		// TODO Auto-generated constructor stub
		this.receiveSocket=receiveSocket;
	}
	
	@Override
	public void run(){
		try {
			while(true){
				byte[] receiveByte=new byte[1024];
				DatagramPacket receivePacket=new DatagramPacket(receiveByte, receiveByte.length);
				receiveSocket.receive(receivePacket);
				String IP=receivePacket.getAddress().getHostName();
				String date=new String(receivePacket.getData());
				int port =receivePacket.getPort();
				System.out.println(IP+"::"+date+"::"+port);
			}
			
		} catch (Exception e) {
			// TODO: handle exception
		}
		
		
	}
	
}
