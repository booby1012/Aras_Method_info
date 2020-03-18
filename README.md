# Aras_Method_info
 Aras上已開發可使用之方法

 //-------------------------------Aras 方法--------------------------------//

# 取得客戶編號(TeamID) :  ts_get_team_customer_list
使用方法 : 
            Parameter : identity (string ,分割)
            Return : customer_list (string ,分割)
ex.
var customer_list =  inn.applyMethod("ts_get_team_customer_list","<identity>"+identity+"</identity>").getResult();

# 取得 組織列表(未來權限/下拉式列表) : ts_get_org_list
使用方法 : 
            <!--Parameter : identity (string ,分割)-->
            Return : org_list (string ,分割)
ex.
<!-- string org_list =  inn.applyMethod("ts_get_org_list","<identity>"+identity+"</identity>"); -->
var org_list =  inn.applyMethod("ts_get_org_list");

# 取得 狀態為已完成之裝櫃實績表頭資料(單張) : ts_get_ContainerActuals_info
使用方法 : 
            Parameter : 組織(string) / 客戶編號(string) / 發票號 (string)
            Return : 
                    Success : CA_details (string ??分割)  ( 櫃號 / 櫃號 / 封條號 / 櫃型 / 備註 / 發票日期 )
                    Fail : Error-1 (string) <!--查無資料-->
                           Error-3 (string) <!--僅能查詢當月表單 該單非當月表單-->
ex.
var CA_details =  inn.applyMethod("ts_get_ContainerActuals_info","<org>"+org+"</org>"
                   +  "<customer_number>"+customer+"</customer_number>"
                   +  "<invoice_number>"+invoice_number+"</invoice_number>").getResult();
ps.組織+發票號有多張，列出任一張

# 取得櫃型列表(下拉式列表) : ts_get_Container_Type_List
使用方法 : 
            <!-- Parameter : no -->
            Return : 
                    Success : 櫃型 (string ,分割)
                    Fail : Error Message (string) 
ex.
var cntr_noList =  inn.applyMethod("ts_get_Container_Type_List").getResult();
ps. 回傳列表為櫃型標籤

# 取得櫃型標籤 : ts_get_container_type_label
使用方法 : 
            Parameter : 該櫃型的值 
            Return : 
                    Success : 櫃型的標籤 (string)) 
ex.
var the_cntrType_label = inn.applyMethod("ts_get_container_type_label","<thevalue>"+thevalue+"</thevalue>").getResult();

# 取得檢核程式負責人的收信者
使用方法 : 
            Parameter : 檢核程式負責人的功能名稱(string) 
            Return : 
                    Success :  信箱(string ,分割)
                    Fail : Error Message (string) 
ex.
string email_list=inn.applyMethod("ts_get_email_from_checking","<title>"+title+"</title>").getResult();
ps. 呼叫Aras方法參數只能傳字串(或Item)，所以getmail只能寫在要寄信的程式下方，我就不放上來了。
ps2.傳item給方法的格式:item.apply("方法名");

# 取得工作流程節點是哪個物件
使用方法 : 
            Parameter : 想要取得的節點id(string) 
            Return : 
                    Success :  物件(Item)
                    Fail : Error Message (string) 
ex.
Item ts_order=inn.applyMethod("ts_GetAppBill","<activity_id>"+節點id+"</activity_id>");
ps. 用來放在節點或路徑上時可以用this.getID()拿到節點id，博威寫的。
ps2.我之前還找到一個用vb寫的相同功能，功能一樣就不放了。

# 編輯 狀態為已完成之裝櫃實績表頭資料(單張) : ts_update_ContainerActuals_info
使用方法 : 
            Parameter : 組織 / 客戶編號 / 發票號 / 櫃號 / 封條號 / 櫃型 / 備註 / 發票日期 (all string)
            Return : 
                    Success : Success (string)
                    Fail :  Error-1. Need parameter org , invoice_number
                            Error-2. Empty edited
                            Error-3. Actual_ship_date Date Error
                            Error-4. Update Error
ex.
var result =  inn.applyMethod("ts_update_ContainerActuals_info","<userid>"+userid+"</userid>" 
                   +  "<org>>"+org+"</org>"  
                   +  "<ts_customer_number>"+ts_customer_number+"</ts_customer_number>" 
                   +  "<ts_invoice_number>"+ts_invoice_number+"</ts_invoice_number>"             
                   +  "<ts_cntr_no>"+ts_cntr_no+"</ts_cntr_no>"
                   +  "<ts_seal_no>"+ts_seal_no+"</ts_seal_no>"
                   +  "<ts_container_type>"+ts_container_type+"</ts_container_type>"
                   +  "<ts_remark>"+ts_remark+"</ts_remark>"
                   +  "<ts_actual_ship_date>"+ts_actual_ship_date+"</ts_actual_ship_date>"
                   ).getResult();
ps.更新紀錄會在裝櫃實績頁籤顯示





