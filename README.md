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
v_TemplateID = "tz2iw419cd32249cd4a32a0dfdd86a67854c1";
r_Fields = zoho.writer.getMergeFields(v_TemplateID,"writer123");
info r_Fields;
m_Data = Map();
m_Data.put("Name",name);
m_MergedData = Map();
m_MergedData.put("merge_data",{"data":m_Data});
outputsettings = Map();
outputsettings.put("doc_name","Fiche_Technique_Climaconfort " + name);
param = Map();
param.put("merge_data",{"data":m_Data});
param.put("output_settings",outputsettings);
response = invokeurl
[
	url :"https://www.zohoapis.in/writer/api/v2/documents/tz2iw419cd32249cd4a32a0dfdd86a67854c1/merge/store"
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
return "Document";
}
 
