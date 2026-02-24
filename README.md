# Automating-Document-Generation-in-Zoho-CRM-with-Zoho-Writer

## 📌 Overview
Excited to share my latest Zoho CRM automation! Using Zoho Writer, I created a custom button that automatically generates a document from a template with CRM data, 
stores it, and updates the record with a shareable link. This simplifies workflows, saves time, and ensures accuracy in document creation. 

## 💡 Client Deluge Code

```java
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
    Country = resp.getJSON("Country");
    Zip_Code = resp.getJSON("Zip_Code");
    City = resp.getJSON("City");

    v_TemplateID = "your_template_id";

    r_Fields = zoho.writer.getMergeFields(v_TemplateID,"writer123");
    info r_Fields;

    m_Data = Map();
    m_Data.put("Name",name);
    m_Data.put("Owner",Owner);
    m_Data.put("Name1",Name1);
    m_Data.put("Phone",Phone);
    m_Data.put("Email",Email);

    m_MergedData = Map();
    m_MergedData.put("merge_data",{"data":m_Data});

    outputsettings = Map();
    outputsettings.put("doc_name","Fiche_Technique_Climaconfort");

    param = Map();
    param.put("merge_data",m_MergedData);
    param.put("output_settings",outputsettings);

    response = invokeurl
    [
        url :"https://www.zohoapis.in/writer/api/v2/documents/"+v_TemplateID+"/merge/store"
        type :POST
        parameters:param
        connection:"writer123"
    ];

    document = response.getJSON("records").getJSON("document_url");

    crmmap = Map();
    crmmap.put("URL_1",document);

    update = zoho.crm.updateRecord("Crm_to_Creator_test",ID,crmmap);

    return "Document Updated Successfully";
}
```
