# tuitui99-rsa
beijing.tuitui99.com密码加密rsa逆向

rsa特点；
```javascript
//第一步
var xxx =new rsa
//第二部
xxx.setPublicKey
//第三步
xxx.调用加密方法('明文')
```
所以改写的时候也需要这几个步骤；

断点，定位到password加密处代码
<img width="1046" alt="image" src="https://user-images.githubusercontent.com/85286900/196903914-a5b68b80-1c9c-4ec6-9644-c34859ce718a.png">
```javascript
        //这个事rsa的publickey，保存下来备用
        login.pubkey='-----BEGIN PUBLIC KEY-----';
        login.pubkey+='MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDAbfx4VggVVpcfCjzQ+nEiJ2DL';
        login.pubkey+='nRg3e2QdDf/m/qMvtqXi4xhwvbpHfaX46CzQznU8l9NJtF28pTSZSKnE/791MJfV';
        login.pubkey+='nucVcJcxRAEcpPprb8X3hfdxKEEYjOPAuVseewmO5cM+x7zi9FWbZ89uOp5sxjMn';
        login.pubkey+='lVjDaIczKTRx+7vn2wIDAQAB';
        login.pubkey+='-----END PUBLIC KEY-----';
        
        //rsa的三步骤代码
        var encrypt = new JSEncrypt();//第一步
        encrypt.setPublicKey(login.pubkey);//第二步
        var encrypted = encrypt.encrypt(password);//第三步，加密方法

```
跟进加密方法，这个比较简单把整个js扣出来；
然后组装下
```javascript
function getpswd(password){
	pubkey='-----BEGIN PUBLIC KEY-----';
	pubkey+='MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDAbfx4VggVVpcfCjzQ+nEiJ2DL';
	pubkey+='nRg3e2QdDf/m/qMvtqXi4xhwvbpHfaX46CzQznU8l9NJtF28pTSZSKnE/791MJfV';
	pubkey+='nucVcJcxRAEcpPprb8X3hfdxKEEYjOPAuVseewmO5cM+x7zi9FWbZ89uOp5sxjMn';
	pubkey+='lVjDaIczKTRx+7vn2wIDAQAB';
	pubkey+='-----END PUBLIC KEY-----';
	var encrypt = new JSEncrypt();
    encrypt.setPublicKey(login.pubkey);
	return encrypt.encrypt(password);
	
}
```
扣下来的代码保存在kou.js
