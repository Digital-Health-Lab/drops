
DROPS Web Portal Use Case demostrates step count data sharing
http://drops.phit.flinders.edu.au:8080/sgd/

1. Signup and login

2. User Profile page

3. Study page
	Add/edit/view/delete your own studies
	View shared studies
	Download zipped data (study + participants' profile + step count data)

4. Source page
	Add/edit/view/delete your own sources

5. Participant page
	Add/edit/view/delete your own participants
	Upload step count data (.csv) against to the selected participant
		1) Prepare CSV dataset
			Mandatory variables:
				timestamp
				steps OR xAxis, yAxis, zAxis
			Optional variables:
				duration, variableName, variableValue
			Timestamp format: dd/MM/yyyy HH:mm:ss

		2) Choose the source from the list
		3) Input default duration in seconds. eg: 86400 is one day
		4) Upload your formated csv file
		
	Download zipped data (participants' profile + step count data)



DROPS API Use Case demostrates universal research data sharing (Signup and add your own study via Web Portal before use API)
http://drops.phit.flinders.edu.au:8080/ands/

Part One: via web browser
1. Authentication to get accessToken
POST:
http://drops.phit.flinders.edu.au:8080/ands/api/v1/auth
HEADER:
Content-Type:application/json
BODY:
{"username":"yang.yang@flinders.edu.au","password":"123123"}
RESPONSE:
accessToken

2. Add research data against a study by studyId
POST:
http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/add
HEADER:
Content-Type:application/json
Authorization:Bearer accessToken
BODY:
{"studyId":1,"variableName":"API add","variableSource":"manual","value":"2000","linkageKey":"120","measuredAt":"27/11/2019 13:22:11"}
RESPONSE:
research data objectId

3. Update research data by research data objectId
PUT:
http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/update
HEADER:
Content-Type:application/json
Authorization:Bearer accessToken
BODY:
{"_id":"5ddde1e5148a7d0682cc270a","studyId":1,"variableName":"API update","variableSource":"manual","value":"3000","linkageKey":"120","measuredAt":"27/11/2019 13:22:11"}

4. List/download research data by studyId
GET:
http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/getbystudy?studyId=1
HEADER:
Authorization:Bearer accessToken

5. List/download research data by userId
GET:
http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/getbyuser?userId=1
HEADER:
Authorization:Bearer accessToken


Part Two: via command terminal
Public Endpoints:
curl -i http://drops.phit.flinders.edu.au:8080/ands/api/v1

curl -i http://drops.phit.flinders.edu.au:8080/ands/api/v1/name/Peter


1. Authentication to get accessToken
curl -i -X POST -H "Content-Type:application/json" http://drops.phit.flinders.edu.au:8080/ands/api/v1/auth -d "{\"username\":\"yang.yang@flinders.edu.au\",\"password\":\"123123\"}"


2. Add research data against a study by studyId
curl -i -X POST -H "Authorization:Bearer accessToken" -H "Content-Type:application/json" http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/add -d "{\"studyId\":1,\"variableName\":\"curl add\",\"variableSource\":\"manual\",\"value\":\"4000\",\"linkageKey\":\"120\",\"measuredAt\":\"27/11/2019 13:22:11\"}"

3. Update research data against by research data objectId
curl -i -X PUT -H "Authorization:Bearer accessToken" -H "Content-Type:application/json" http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/update -d "{\"_id\":\"5dddfe3f148a7d0682cc271a\",\"studyId\":1,\"variableName\":\"curl update\",\"variableSource\":\"manual\",\"value\":\"5000\",\"linkageKey\":\"120\",\"measuredAt\":\"27/11/2019 13:22:11\"}"

4. List/download research data by studyId
curl -i -H "Authorization:Bearer accessToken" http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/getbystudy?studyId=1

5. List/download research data by userId
curl -i -H "Authorization:Bearer accessToken" http://drops.phit.flinders.edu.au:8080/ands/api/v1/data/getbyuser?userId=1
