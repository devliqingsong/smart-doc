<%if(isNotEmpty(projectName)){%>

# ${projectName}

<%}%>

<%if(isNotEmpty(revisionLogList)){%>
Version |Update Time |Status |Author |Description
---|---|---|---|---
<% for(revisionLog in revisionLogList){ %>
${revisionLog.version} |${revisionLog.revisionTime} |${revisionLog.status} |${revisionLog.author} |${revisionLog.remarks}
<%}%>

<%}%>

<%if(isNotEmpty(dependencyList)){%>

## Add dependency

```
<%
for(dependency in dependencyList){
%>
<dependency>
    <groupId>${dependency.groupId}</groupId>
    <artifactId>${dependency.artifactId}</artifactId>
    <version>${dependency.version}</version>
</dependency>

<%}%>
```

<%if(isNotEmpty(consumerConfigExample)){%>
Consumer config

```
${consumerConfigExample}
```

<%}%>
<%}%>

<% for(api in apiDocList){ %>

## ${htmlEscape(api.desc)}

**URI:** ${api.uri}

**Service:** ${api.name}

**Protocol:** ${api.protocol}

**Author:** ${api.author}

**Version:** ${api.version}
<% for(doc in api.list){ %>
<%if(doc.deprecated){%>

### ~~${htmlEscape(doc.desc)}~~

<%}else{%>

### ${htmlEscape(doc.desc)}

<%}%>

**Definition：** ${doc.methodDefinition}

<%if(isNotEmpty(doc.author)){%>
**Author:** ${doc.author}
<%}%>

**Description:** ${doc.detail}

<%if(isNotEmpty(doc.requestParams)){%>
**Invoke-parameters:**

Parameter|Type|Description|Required|Since
---|---|---|---|---
<% for(param in doc.requestParams){ %>
${param.field}|${param.type}|${param.desc}|${param.required}|${param.version}
<%}%>
<%}%>

<%if(isNotEmpty(doc.responseParams)){%>
**Response-fields:**

Field | Type|Description|Since
---|---|---|---
<% for(param in doc.responseParams){ %>
${param.field}|${param.type}|${param.desc}|${param.version}
<%}%>
<%}%>

<%}%>
<%}%>
<%if(isNotEmpty(errorCodeList)){%>
## ${errorListTitle}

Error code |Description
---|---
<% for(error in errorCodeList){ %>
${error.value}|${htmlEscape(error.desc)}
<%}%>

<%}%>

<%if(isNotEmpty(dictList)){%>
## ${dictListTitle}

<% for(dict in dictList){ %>
### ${dict.title}
Code |Type|Description 
---|---|---
<% for(dataDict in dict.dataDictList){ %>
${dataDict.value}|${dataDict.type}|${htmlEscape(dataDict.desc)}
<%}%>

<%}%>
<%}%>
