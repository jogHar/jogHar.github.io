---
layout: post
title:  "MAC Address by Java"
date:   2020-10-31 12:37:11 +0530
categories: []
tags: mac-address java
author: "Hardik Jogani"
---

If you can try to find 'MAC address' by java code, so this blog is for you.

In this code, I use [NetworkInterface](https://docs.oracle.com/javase/7/docs/api/java/net/NetworkInterface.html) class and [getHardwareAddress](https://docs.oracle.com/javase/7/docs/api/java/net/NetworkInterface.html#getHardwareAddress()) method.

In ubuntu, I use 'wlp2s0' and 'enp1s0' respectively for wireless network and ethernet. if you want to know more about use this [article](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/). 

``` java
import java.net.InetAddress;
import java.net.NetworkInterface;

/**
 * @author jogHar
 */
public class SystemMacAddress {
    public static String getSystemMac(){
        try{
            String OSName=  System.getProperty("os.name");
            if(OSName.contains("Windows")){
                return (getMAC4Windows());
            } else{
                String mac=getMAC4Linux("wlp2s0");
                if(mac==null){
                    mac=getMAC4Linux("enp1s0");
                }	
                return mac;
            }
        }
        catch(Exception E){
            System.err.println("System Mac Exp : "+E.getMessage());
            return null;
        }
    }
    
    /**
     * Method for get MAc of Linux Machine
     */
    private static String getMAC4Linux(String name){
        try {
            NetworkInterface network = NetworkInterface.getByName(name);
            byte[] mac = network.getHardwareAddress();
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < mac.length; i++){
                sb.append(String.format("%02X%s", mac[i], (i < mac.length - 1) ? "-" : ""));        
            }
            return (sb.toString());
        }
        catch (Exception E) {
            System.err.println("System Linux MAC Exp : "+E.getMessage());
            return null;
        } 
    } 
	
    /**
     * Method for get Mac Address of Windows Machine
     */
    private static String getMAC4Windows(){
        try{
            InetAddress addr =InetAddress.getLocalHost();
            NetworkInterface network = NetworkInterface.getByInetAddress(addr);

            byte[] mac = network.getHardwareAddress();

            StringBuilder sb = new StringBuilder();
            for(int i=0;i<mac.length;i++){
                sb.append(String.format("%02X%s", mac[i], (i < mac.length - 1) ? "-" : ""));		
            }
            return sb.toString();
        }
        catch(Exception E){
            System.err.println("Windows MAC : "+E.getMessage());
            return null;
        }
    }
  
    public static void main(String[] args) {
        String macAddress = getSystemMac();
        System.out.println("System Mac Address : "+macAddress);
    }
    
}
```