Instructions:

I found a decision how to show all your passwords from Chromium. Tested on Chromium: 

> Version 40.0.2214.111 Ubuntu 14.04 (64-bit) -  Passed

> Version 43.0.2357.65 Built on 8.0, running on Debian 8.1 (64-bit) - Passed

> Version 48.0.2564.82 Built on 8.3, running on Debian 8.3 (64-bit) - Passed

I used js script found early in search.


Output format changed for ready to use in FireFox Export plugin 
Please install this plugin from https://addons.mozilla.org/en-Us/firefox/addon/password-exporter/

Output maked in format: 
"hostname","username","password","formSubmitURL","httpRealm","usernameField","passwordField"

Last 3 fields "httpRealm","usernameField","passwordField" filled empty because Chrome has no information about in his Chrome Password Manager.


1.Open in Chromium browser link to Chrome password manager: **chrome://settings-frame/passwords**

2.Open console (F12) and insert this js code:
```
  var out="";
  var out2="";
  var pm = PasswordManager.getInstance();
  var model = pm.savedPasswordsList_.dataModel;
  var pl = pm.savedPasswordsList_;
  for(i=0;i<model.length;i++){
   PasswordManager.requestShowPassword(i);
  };
  setTimeout(function(){
  out2+='# Generated by Password Exporter; Export format 1.1; Encrypted: false\n';
  out2+='"hostname","username","password","formSubmitURL","httpRealm","usernameField","passwordField"';
  for(i=0;i<model.length;i++){
  var item = pl.getListItemByIndex(i);
  out+="\n"+model.array_[i][0]+"|"+model.array_[i][1]+"|"+item.childNodes[0].childNodes[2].childNodes[0].value;
  out2+='<br/>"http://'+model.array_[i][0]+'","'+model.array_[i][1]+'","'+item.childNodes[0].childNodes[2].childNodes[0].value+'","http://'+model.array_[i][0]+'"," "," "," "';
  };
  document.write(out2);
  },300);
```

3.Now you see all your passwords in format i described early.

4.Copy all data to csv file and import to FireFox :)

5.Profit
