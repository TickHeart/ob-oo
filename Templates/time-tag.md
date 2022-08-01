<%*

	let today = tp.date.now("YYYY-MM-DD") 
	let titleName = tp.file.title
	
	if (titleName === "未命名" | titleName === "Untitled") {
		let inputDate = await tp.system.prompt("请输入文件名称和标签：" + today,"")
		titleName = inputDate
	}
	
	let createTime = tp.file.creation_date() 
	
	let modificationDate = tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") 
	
	const tagList = titleName.split("-")
	
	let tags = tagList.length > 0 ? tagList.filter((item, index) => index > 0).map((item) => ` #${item.replace(/\s/gm, '')}`).join("") : ""
	
	await tp.file.rename(`${tagList[0]}`)
	
-%>
---

create_time : <% createTime %>

modification_date: <% modificationDate %>

---
<% tags %>
