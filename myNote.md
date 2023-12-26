# 修改檔案時間 
``` powershell
Set-ItemProperty -Path <文件路徑> -Name LastWriteTime -Value <新日期和時間>
Set-ItemProperty -Path filepath+filename -Name LastWriteTime -Value '2023/10/22 12:42'
Set-ItemProperty -Path d:\test.exe -Name LastWriteTime -Value '2023/09/27 10:13'
```
# 表單常用的語法集
## 以docid 及登入者ID 開啟文管系統
``` javascript
    var vMEM = Client.getCurrentMember();	
	var vLoginID =vMEM.getLoginID();
	var host = Client.getServerEnv().getWebAgendaURL();
	var ls_url = host+"/docSSO.jsp?key="+vDocKey+"&openType=openIndex&userID="+vLoginID;		
	Form.openWin(ls_url, "原物料供應商評鑑表", "width=800, height=600,scrollbars=yes, status=yes, resizable=yes"); 
```
## SQL 傳參數的方式
```
var vSQL ="select MEM.EMAIL EMAIL from a_parameter_data para , mem_geninf mem  where para.parameter ='PR_PO'  and para.remarks = '量測儀器' and ";
		vSQL+=" para.KEY1 = ? and PARA.VALUE2 = MEM.MEMID and MEM.RESIGN = 'false'" ;	
   var args = [vNAME];		
	var vec = Server.SQLloadValue(vSQL , args); 
	if(vec != null && vec.size() > 0){
		for(var i=0;i<vec.size();i++){
			vReturn = vReturn + vec.get(i).get("EMAIL")+";"
		}		
	}
```
## 表格選取
```javascript
    // 以下是開窗選取程式清單,將選取的項目回寫母表單的Table
    var parentform = Form.getParentForm();
	var vParentTable = parentform.getComponent("PRGList");	
	var table = Form.getComponent("PRGList");
	var vec = table.checkedRows;  //vec 存的是選取的 rowid 
	if(vec.size()>0){
		vParentTable.clear();
		for(i = 0 ;i < vec.size();i++){
			var vPRGID = table.getValueAt(vec.get(i) ,"程式編號");
			var vPRNAME = table.getValueAt(vec.get(i) ,"程式名稱");
			var vPRDESC = table.getValueAt(vec.get(i),"描述");										
			var row = vParentTable.newRow()-1;					
			vParentTable.setValueAt(vPRGID,row,"程式編號");
			vParentTable.setValueAt(vPRNAME,row,"程式名稱");
			vParentTable.setValueAt(vPRDESC,row,"描述");		
		}
		Form.refreshParent();
		Form.closeForm();				
	}else{
		Form.showMessageDialog("請先選取程式清單再點擊取回！");
	}    
```
## 表單call Teamp+ 
```javascript
var text = "   您 好: \n";
		text += "   \n";
		text += "   ePO 流程結束寫入ERP TempTable 失敗。\n";
		text += "   流程名稱 : " + Server.getTask(MyTask.getParentID()).getProcessName()  +"\n";
		text += "   工作名稱 : " + MyTask.getProcessName()  +"\n";
		text += "   申請人 : " + dataMap.get("App_Name")  	+"\n";
		text += "   單號 : " + dataMap.get("ANS")  	+"\n";
		text += "   INSID :" + dataMap.get("PO_INSID")  	+"\n";
		text += "   填單日期 : " + dataMap.get("Create_Date")  	+"\n";

var UrlPostTest = new Packages.ext.UrlPostTest();
var response_msg = UrlPostTest.sendSuperHubMsg(ch_sn, api_key,content_type,text+text_content,media_content,file_show_name,msg_push,account_list);
```
# loadLibrary("com.gce.Common.Util");
## 以廠別取ERP ORGID
**type : vType-> INV  -->31 ; FIN --> 30**
``` Javascript
var vORGID = ClientGetERPORGID(vFactory, vType)' // Client side
var vORGID = ServerGetERPORGID(vFactory, vType)' // Server side
```
# loadLibrary("com.A.Common.Client.Util");
## SQL Injection  Test
``` javascript
if(!isSqlInjection( ISANO )){return ' and 1=2'} ;
```
## 廠務總經理
**vType username -->中文姓名 or memid**
``` javascript
 getMFGManager(vFactory , vType)
```
