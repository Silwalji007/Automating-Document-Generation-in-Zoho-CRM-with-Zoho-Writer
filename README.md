# Automating-Document-Generation-in-Zoho-CRM-with-Zoho-Writer

## 📌 Overview
Excited to share my latest Zoho CRM automation! Using Zoho Writer, I created a custom button that automatically generates a document from a template with CRM data, 
stores it, and updates the record with a shareable link. This simplifies workflows, saves time, and ensures accuracy in document creation. 

---

## 💡 Client Deluge Code

string button.URL_LINK1(String ID)
{
resp = zoho.crm.getRecordById("Crm_to_Creator_test",ID);
info resp;
name = resp.getJSON("Name");
Owner = resp.getJSON("Owner");
Name1 = resp.getJSON("Name1");
Phone = resp.getJSON("Phone");
Email = resp.getJSON("Email");
DOB = resp.getJSON("DOB");
Street = resp.getJSON("Street");
Company_Name = resp.getJSON("Company_Name");
Street = resp.getJSON("Street");
Country = resp.getJSON("Country");
Zip_Code = resp.getJSON("Zip_Code");
City = resp.getJSON("City");
v_TemplateID = "tz2iwe121aeab8f674a9bb12a60d21342447f";
r_Fields = zoho.writer.getMergeFields(v_TemplateID,"writer123");
info r_Fields;
m_Data = Map();
m_Data.put("Name",name);
m_Data.put("Owner",Owner);
m_Data.put("Name1",Name1);
m_Data.put("Phone",Phone);
m_Data.put("Email",Email);
m_Data.put("DOB",DOB);
m_Data.put("Street",Street);
m_Data.put("Company_Name",Company_Name);
m_Data.put("Street",Street);
m_Data.put("Country",Country);
m_Data.put("Zip_Code",Zip_Code);
m_Data.put("City",City);
m_MergedData = Map();
m_MergedData.put("merge_data",{"data":m_Data});
outputsettings = Map();
outputsettings.put("doc_name","Fiche_Technique_Climaconfort " + name);
param = Map();
param.put("merge_data",{"data":m_Data});
param.put("output_settings",outputsettings);
response = invokeurl
[
	url :"https://www.zohoapis.in/writer/api/v2/documents/tz2iwe121aeab8f674a9bb12a60d21342447f/merge/store"
	type :POST
	parameters:param
	connection:"writer123"
];
info response;
documentt = response.getJSON("records").getJSON("document_url");
info "documentt Url>>>" + documentt;
crmmap = Map();
crmmap.put("URL_1",documentt);
update = zoho.crm.updateRecord("Crm_to_Creator_test",ID,crmmap);
info update;
return "Document Updated Successfully";
}
