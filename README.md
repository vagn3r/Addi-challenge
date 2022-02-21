# Addi-challenge
## A README as a runbook explaining how to carry out the process.

### 1. Download Ubuntu ISO.
```
https://ubuntu.com/download/desktop
```
### 2. Download and install VirtualBox.
```
https://www.virtualbox.org/wiki/Downloads
```
### 3. Create Ubuntu VM.
Attach .ISO file for media boot, then follow Ubuntu installation

### 4. Setup environment.
Install Docker
```
sudo apt-get update
sudo apt-get install \
  ca-certificates \
  curl \
  gnupg \
  lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
Test Docker
```
sudo docker run hello-world
```
Install DBeaver
```
sudo add-apt-repository ppa:serge-rider/dbeaver-ce
sudo apt-get update
sudo apt-get install dbeaver-ce
```
### 5. Follow "How to run this app in local environment" steps.
---
## Deliverables
### 1. SQL script to add a new ally.
```
insert into stores(id, "data")
values (1234567890, '{"name": "Aliado ADDI", "brand": "Merchant", "minAMount": 20, "maxAmount": 150,
"discount": 5, "tags": ["tecnologia", "informacion", "finanzas"], "credentials": null}')
```
### 2. SQL query to list all allies with the tag "finance" ("finanzas")
```
select s."data"->>'name' as name
from stores s where data->>'tags' like '%finanzas%'
```
### 3. HTTP Request that adds a given ally's credentials through our API
```
curl -d '{"username": "addi","password": "123456"}' -H "Content-Type: application/json" -X POST http://127.0.0.1:5000/allies/1234567890/credentials
```
#### 3.1 Console result
<pre><font color="#4E9A06"><b>vagner@vg-vBox</b></font>:<font color="#3465A4"><b>~</b></font>$ curl -d &apos;{&quot;username&quot;: &quot;addi&quot;,&quot;password&quot;: &quot;123456&quot;}&apos; -H &quot;Content-Type: application/json&quot; -X POST http://127.0.0.1:5000/allies/1234567890/credentials
{
  &quot;AllyId&quot;: &quot;1234567890&quot;, 
  &quot;AllyName&quot;: &quot;Aliado ADDI&quot;, 
  &quot;message&quot;: &quot;Credentials added&quot;
}</pre>
#### 3.2 DB data record result:
<pre>
{"name": "Aliado ADDI", "tags": ["tecnologia", "informacion", "finanzas"], "brand": "Merchant", "discount": 5, "maxAmount": 150, "minAMount": 20, "credentials": "pbkdf2:sha256:260000$KxSjQ7P3zqwuNkhk$7e907dca5ffa52c1f5f7c76d699cc5aff4c00f0cdedcd23855d3096d6a1cefdd"}
</pre>
#### 3.3 HTTP request that checks ally's credentials through our API
```
curl http://127.0.0.1:5000/allies/1234567890/credentials
```
##### 3.3.1 Console result
<pre><font color="#4E9A06"><b>vagner@vg-vBox</b></font>:<font color="#3465A4"><b>~</b></font>$ curl http://127.0.0.1:5000/allies/1234567890/credentials
{
  &quot;message&quot;: &quot;Ally has credentials set!&quot;
}</pre>
