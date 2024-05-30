---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
Master ^5UTaNV4T

USER ^DyUldmW8

Router ^5zZnVsJk

JD CV match ^mIjreD2m

JD Tool ^iu8haW0J

Confirmation ^3VoNuuHv

Human in the loop ^im8bapwa

State:
1. CV Details
2. Current JD
3. New JD
4. Extracted Details
5. Memory (summary)
6. Sender (for router) ^I3dkHDCI

Entire Graph Can Access the state
1. When we are starting the chats,
first we have to fetch cv details and 
current JD details and save into memory

CV Tool: write a function to fetch current 
cv details, is data not available in state
JD Details: same as cv ^tDVePyGn

Model: Google Gemini 1.5 pro or flash
Model Instruction: offtopic should not be 
discussed ^5Ud0eHqy

Only if user share CV
then route to this node ^dlgVevMa

When user looking for a change
route here ^YgGcNJtz

Reference
1. Human in the loop
2. Persistence
3. Basic Multiagent Collaboration ^uZGW3Jsy

Instructions:
1. Use google gemini 1.5
2. Use langsmit for tracking
3. Use sql file (not memory) to session persistence
4. For JD, create sql db populate values, table
    - name
    - id
    - designation
    - skills
    - years of exp

5. JD Tool should access the data from this new JD
database ^fbGfUmj1

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.1.7",
	"elements": [
		{
			"type": "ellipse",
			"version": 229,
			"versionNonce": 488139141,
			"index": "a0",
			"isDeleted": false,
			"id": "SbZBXt0NSX62yD8wtwetN",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -226.25,
			"y": -242.2578125,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 223,
			"height": 201,
			"seed": 1611493636,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "5UTaNV4T"
				},
				{
					"id": "oALaHVG8uq6l1K_hm_nlS",
					"type": "arrow"
				},
				{
					"id": "QFxfquLveZ81mOf5ujFMz",
					"type": "arrow"
				},
				{
					"id": "Mlfq2sPm1uwVnNnXUKQRm",
					"type": "arrow"
				},
				{
					"id": "qH3TZIQEJPdNBmJYujt5E",
					"type": "arrow"
				},
				{
					"id": "qkZtXXTdxFWnwDNswNM48",
					"type": "arrow"
				},
				{
					"id": "X2ZQWzcOifTeUfO6UqfE6",
					"type": "arrow"
				}
			],
			"updated": 1716365995137,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 121,
			"versionNonce": 457412028,
			"index": "a0V",
			"isDeleted": false,
			"id": "5UTaNV4T",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -149.77236826050319,
			"y": -154.32204400924803,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 70.35992431640625,
			"height": 25,
			"seed": 374592132,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716359036717,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Master",
			"rawText": "Master",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "SbZBXt0NSX62yD8wtwetN",
			"originalText": "Master",
			"lineHeight": 1.25
		},
		{
			"type": "ellipse",
			"version": 120,
			"versionNonce": 632984728,
			"index": "aP",
			"isDeleted": false,
			"id": "K8ebl8oDoJKbtAxMZ6grX",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "dotted",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 71.61562793219775,
			"y": -426.6597829799997,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 156.14754500511435,
			"height": 161.8953073979407,
			"seed": 1526222232,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "DyUldmW8"
				},
				{
					"id": "oALaHVG8uq6l1K_hm_nlS",
					"type": "arrow"
				},
				{
					"id": "0JcWIDo52d7J4ilXvj9qN",
					"type": "arrow"
				}
			],
			"updated": 1716361512795,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 49,
			"versionNonce": 1950367429,
			"index": "aQ",
			"isDeleted": false,
			"id": "DyUldmW8",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 122.74293911918953,
			"y": -358.4507641327116,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 53.47993469238281,
			"height": 25,
			"seed": 497888488,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716365870555,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "USER",
			"rawText": "USER",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "K8ebl8oDoJKbtAxMZ6grX",
			"originalText": "USER",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 104,
			"versionNonce": 1283279711,
			"index": "aR",
			"isDeleted": false,
			"id": "oALaHVG8uq6l1K_hm_nlS",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 81.26372764784648,
			"y": -282.5218655462155,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 93.39228926848419,
			"height": 76.84113330772215,
			"seed": 946977432,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710718,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "K8ebl8oDoJKbtAxMZ6grX",
				"gap": 13.776463804454664,
				"focus": -0.06668321473687956
			},
			"endBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 12.795123450484908,
				"focus": 0.15073848969099343
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-93.39228926848419,
					76.84113330772215
				]
			]
		},
		{
			"type": "ellipse",
			"version": 129,
			"versionNonce": 1430367275,
			"index": "aT",
			"isDeleted": false,
			"id": "zSZ8Pfb09edupUhY2nAG5",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 116.63976667600355,
			"y": -184.29580208249087,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 169.55899058837588,
			"height": 153.2736638087012,
			"seed": 305410200,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "5zZnVsJk"
				},
				{
					"id": "QFxfquLveZ81mOf5ujFMz",
					"type": "arrow"
				},
				{
					"id": "_43zeu_EemyuubRTWGVVR",
					"type": "arrow"
				},
				{
					"id": "DgBIgKwKt-2l29TD2P_8M",
					"type": "arrow"
				},
				{
					"id": "c3GuxR7vGcvjO1uQqFjwg",
					"type": "arrow"
				},
				{
					"id": "0JcWIDo52d7J4ilXvj9qN",
					"type": "arrow"
				},
				{
					"id": "X2ZQWzcOifTeUfO6UqfE6",
					"type": "arrow"
				},
				{
					"id": "cLdn3CjIWMg9TWhsw2MT9",
					"type": "arrow"
				}
			],
			"updated": 1716366000318,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 31,
			"versionNonce": 791804056,
			"index": "aU",
			"isDeleted": false,
			"id": "5zZnVsJk",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 168.05114592012555,
			"y": -120.34939370636013,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 66.83992004394531,
			"height": 25,
			"seed": 838597096,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361510763,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Router",
			"rawText": "Router",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "zSZ8Pfb09edupUhY2nAG5",
			"originalText": "Router",
			"lineHeight": 1.25
		},
		{
			"type": "ellipse",
			"version": 62,
			"versionNonce": 1382361835,
			"index": "aV",
			"isDeleted": false,
			"id": "poykHqfjjrin83MrbeBy3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 411.69156950775346,
			"y": -191.95948527292592,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 190.63411936207217,
			"height": 172.43287178478897,
			"seed": 2141783016,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "mIjreD2m"
				},
				{
					"id": "_43zeu_EemyuubRTWGVVR",
					"type": "arrow"
				},
				{
					"id": "cLdn3CjIWMg9TWhsw2MT9",
					"type": "arrow"
				}
			],
			"updated": 1716366000317,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 40,
			"versionNonce": 560256408,
			"index": "aW",
			"isDeleted": false,
			"id": "mIjreD2m",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 476.3593128137496,
			"y": -130.70727584977882,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 61.49995422363281,
			"height": 50,
			"seed": 1370639768,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716360920906,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "JD CV\nmatch",
			"rawText": "JD CV match",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "poykHqfjjrin83MrbeBy3",
			"originalText": "JD CV match",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 77,
			"versionNonce": 1933124575,
			"index": "aX",
			"isDeleted": false,
			"id": "QFxfquLveZ81mOf5ujFMz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 6.351857723839515,
			"y": -118.62700796898565,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 88.30070004923934,
			"height": 1.8813240887197793,
			"seed": 919737832,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710718,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 12.23439037247772,
				"focus": 0.20442821869095726
			},
			"endBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 22.439099854500313,
				"focus": 0.08886149983117718
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					88.30070004923934,
					1.8813240887197793
				]
			]
		},
		{
			"type": "arrow",
			"version": 79,
			"versionNonce": 1396220319,
			"index": "aY",
			"isDeleted": false,
			"id": "_43zeu_EemyuubRTWGVVR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 300.4975417764837,
			"y": -116.05261817239571,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 98.68541720892716,
			"height": 4.3977388297450375,
			"seed": 405622760,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710720,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 14.71963867725377,
				"focus": -0.1669323708958692
			},
			"endBinding": {
				"elementId": "poykHqfjjrin83MrbeBy3",
				"gap": 12.701695977089983,
				"focus": 0.012821585069651682
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					98.68541720892716,
					4.3977388297450375
				]
			]
		},
		{
			"type": "ellipse",
			"version": 106,
			"versionNonce": 379206808,
			"index": "aZ",
			"isDeleted": false,
			"id": "YiHJc3RzOflCMUm5yoIo4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 236.3848165265515,
			"y": 82.01718878512759,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 153.27366380870126,
			"height": 132.19853503500485,
			"seed": 1632623768,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "iu8haW0J"
				},
				{
					"id": "DgBIgKwKt-2l29TD2P_8M",
					"type": "arrow"
				}
			],
			"updated": 1716360993855,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 66,
			"versionNonce": 911665560,
			"index": "aa",
			"isDeleted": false,
			"id": "iu8haW0J",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 271.9412636600065,
			"y": 135.37721600954035,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 81.77992248535156,
			"height": 25,
			"seed": 1792010136,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716360993855,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "JD Tool",
			"rawText": "JD Tool",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "YiHJc3RzOflCMUm5yoIo4",
			"originalText": "JD Tool",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 180,
			"versionNonce": 1400330783,
			"index": "ac",
			"isDeleted": false,
			"id": "DgBIgKwKt-2l29TD2P_8M",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 236.211904210529,
			"y": -20.873214521139502,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 55.776766806012375,
			"height": 100.57721123652233,
			"seed": 1206910616,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710720,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 15.852740920391994,
				"focus": 0.14062555671968685
			},
			"endBinding": {
				"elementId": "YiHJc3RzOflCMUm5yoIo4",
				"gap": 4.720751158957242,
				"focus": 0.1990091368350612
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					55.776766806012375,
					100.57721123652233
				]
			]
		},
		{
			"type": "ellipse",
			"version": 46,
			"versionNonce": 1512754072,
			"index": "ad",
			"isDeleted": false,
			"id": "mfzeXGaj7YzeNV9QXLKjT",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 18.927805997956625,
			"y": 92.55475317197568,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 145.60998061826615,
			"height": 117.82912905293904,
			"seed": 426825624,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "text",
					"id": "3VoNuuHv"
				},
				{
					"id": "c3GuxR7vGcvjO1uQqFjwg",
					"type": "arrow"
				},
				{
					"id": "Mlfq2sPm1uwVnNnXUKQRm",
					"type": "arrow"
				}
			],
			"updated": 1716361014518,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 22,
			"versionNonce": 1698925464,
			"index": "ae",
			"isDeleted": false,
			"id": "3VoNuuHv",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 50.75193973164801,
			"y": 126.31042961112618,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 81.99990844726562,
			"height": 50,
			"seed": 134154472,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361006356,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Confirma\ntion",
			"rawText": "Confirmation",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "mfzeXGaj7YzeNV9QXLKjT",
			"originalText": "Confirmation",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 77,
			"versionNonce": 525377119,
			"index": "af",
			"isDeleted": false,
			"id": "c3GuxR7vGcvjO1uQqFjwg",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 146.32864084850073,
			"y": -36.586694759024866,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 34.105476907406114,
			"height": 112.39917866071976,
			"seed": 925048040,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710721,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 10.481334267118953,
				"focus": 0.38135727795039676
			},
			"endBinding": {
				"elementId": "mfzeXGaj7YzeNV9QXLKjT",
				"gap": 18.71296944299739,
				"focus": -0.032898437102765125
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-34.105476907406114,
					112.39917866071976
				]
			]
		},
		{
			"type": "arrow",
			"version": 40,
			"versionNonce": 1280692895,
			"index": "ag",
			"isDeleted": false,
			"id": "Mlfq2sPm1uwVnNnXUKQRm",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -48.13417852898405,
			"y": -52.10367997789402,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 107.30557143523016,
			"height": 144.67090434571202,
			"seed": 455288216,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710721,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 7.638359612059148,
				"focus": -0.0008752582138149307
			},
			"endBinding": {
				"elementId": "mfzeXGaj7YzeNV9QXLKjT",
				"gap": 5.800952464619073,
				"focus": 0.13104773592665167
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					107.30557143523016,
					144.67090434571202
				]
			]
		},
		{
			"type": "text",
			"version": 40,
			"versionNonce": 331959704,
			"index": "ah",
			"isDeleted": false,
			"id": "im8bapwa",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 13.180043605130209,
			"y": 222.83736740937195,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 170.8397979736328,
			"height": 25,
			"seed": 867687656,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361030086,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Human in the loop",
			"rawText": "Human in the loop",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Human in the loop",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 66,
			"versionNonce": 174391448,
			"index": "am",
			"isDeleted": false,
			"id": "zd40h5xEf03qL0ojH9pik",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -528.0675817193459,
			"y": -217.82441604064417,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 239.4900997010957,
			"height": 236.61621850468254,
			"seed": 37187480,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "qH3TZIQEJPdNBmJYujt5E",
					"type": "arrow"
				},
				{
					"id": "qkZtXXTdxFWnwDNswNM48",
					"type": "arrow"
				},
				{
					"type": "text",
					"id": "I3dkHDCI"
				}
			],
			"updated": 1716361146217,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 166,
			"versionNonce": 2078495384,
			"index": "amV",
			"isDeleted": false,
			"id": "I3dkHDCI",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -517.312407662255,
			"y": -187.0163067883029,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 217.97975158691406,
			"height": 175,
			"seed": 1058107880,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361546665,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "State:\n1. CV Details\n2. Current JD\n3. New JD\n4. Extracted Details\n5. Memory (summary)\n6. Sender (for router)",
			"rawText": "State:\n1. CV Details\n2. Current JD\n3. New JD\n4. Extracted Details\n5. Memory (summary)\n6. Sender (for router)",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "zd40h5xEf03qL0ojH9pik",
			"originalText": "State:\n1. CV Details\n2. Current JD\n3. New JD\n4. Extracted Details\n5. Memory (summary)\n6. Sender (for router)",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 42,
			"versionNonce": 340457183,
			"index": "an",
			"isDeleted": false,
			"id": "qH3TZIQEJPdNBmJYujt5E",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -284.7456404230327,
			"y": -135.43982174346718,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 34.48686750167727,
			"height": 0,
			"seed": 2113843096,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710722,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zd40h5xEf03qL0ojH9pik",
				"gap": 3.8318415952174973,
				"focus": -0.30364372469635564
			},
			"endBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 24.183081063781174,
				"focus": -0.06286557966699328
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					34.48686750167727,
					0
				]
			]
		},
		{
			"type": "arrow",
			"version": 58,
			"versionNonce": 267651871,
			"index": "ao",
			"isDeleted": false,
			"id": "qkZtXXTdxFWnwDNswNM48",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -225.34013071792714,
			"y": -90.41568299966121,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 50.78386611586615,
			"height": 0,
			"seed": 529918184,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710722,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 12.612120503708411,
				"focus": -0.5108669602023761
			},
			"endBinding": {
				"elementId": "zd40h5xEf03qL0ojH9pik",
				"gap": 12.453485184456895,
				"focus": 0.07692307692307733
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-50.78386611586615,
					0
				]
			]
		},
		{
			"type": "arrow",
			"version": 199,
			"versionNonce": 503321823,
			"index": "ap",
			"isDeleted": false,
			"id": "0JcWIDo52d7J4ilXvj9qN",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 192.59527909772044,
			"y": -184.88393825908162,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 23.06485218169169,
			"height": 66.55033694258088,
			"seed": 1893475992,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710719,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 1,
				"focus": 0.20193502768216776
			},
			"endBinding": {
				"elementId": "K8ebl8oDoJKbtAxMZ6grX",
				"gap": 15.522685346266996,
				"focus": 0.15469334466201964
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-23.06485218169169,
					-66.55033694258088
				]
			]
		},
		{
			"type": "text",
			"version": 322,
			"versionNonce": 1929337496,
			"index": "ar",
			"isDeleted": false,
			"id": "tDVePyGn",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -509.86633414206267,
			"y": 73.3955451958883,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 433.299560546875,
			"height": 200,
			"seed": 1481500136,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716362152815,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Entire Graph Can Access the state\n1. When we are starting the chats,\nfirst we have to fetch cv details and \ncurrent JD details and save into memory\n\nCV Tool: write a function to fetch current \ncv details, is data not available in state\nJD Details: same as cv",
			"rawText": "Entire Graph Can Access the state\n1. When we are starting the chats,\nfirst we have to fetch cv details and \ncurrent JD details and save into memory\n\nCV Tool: write a function to fetch current \ncv details, is data not available in state\nJD Details: same as cv",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Entire Graph Can Access the state\n1. When we are starting the chats,\nfirst we have to fetch cv details and \ncurrent JD details and save into memory\n\nCV Tool: write a function to fetch current \ncv details, is data not available in state\nJD Details: same as cv",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 92,
			"versionNonce": 1598002072,
			"index": "at",
			"isDeleted": false,
			"id": "IwCkKCpO_LFU6ez63ombh",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -537.6471857073898,
			"y": -449.65083255130503,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 498.1394073782792,
			"height": 128.36669343978735,
			"seed": 2032759960,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1716361581912,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 196,
			"versionNonce": 46140312,
			"index": "aw",
			"isDeleted": false,
			"id": "5Ud0eHqy",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -518.4879777313021,
			"y": -425.7018225811954,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 417.13958740234375,
			"height": 75,
			"seed": 1566773992,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361701238,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Model: Google Gemini 1.5 pro or flash\nModel Instruction: offtopic should not be \ndiscussed",
			"rawText": "Model: Google Gemini 1.5 pro or flash\nModel Instruction: offtopic should not be \ndiscussed",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Model: Google Gemini 1.5 pro or flash\nModel Instruction: offtopic should not be \ndiscussed",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 258,
			"versionNonce": 1787382936,
			"index": "ax",
			"isDeleted": false,
			"id": "_vNctgUedcIUSVXkdIxDU",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 232.55297493133412,
			"y": -281.0498023617337,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 230.8684561118564,
			"height": 85,
			"seed": 1580467608,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "dlgVevMa"
				},
				{
					"id": "Cp1SqtA5lI1biKmcHEKAP",
					"type": "arrow"
				}
			],
			"updated": 1716361857073,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 74,
			"versionNonce": 1508112792,
			"index": "ay",
			"isDeleted": false,
			"id": "dlgVevMa",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 242.38732658345373,
			"y": -276.0498023617337,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 211.1997528076172,
			"height": 75,
			"seed": 747854824,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716361857073,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Only if user share CV\nthen route to this\nnode",
			"rawText": "Only if user share CV\nthen route to this node",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "_vNctgUedcIUSVXkdIxDU",
			"originalText": "Only if user share CV\nthen route to this node",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 50,
			"versionNonce": 2091077439,
			"index": "az",
			"isDeleted": false,
			"id": "Cp1SqtA5lI1biKmcHEKAP",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 341.2929963958464,
			"y": -189.34407957010313,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 2.3833847967959514,
			"height": 56.778139023048595,
			"seed": 915760872,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710722,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "_vNctgUedcIUSVXkdIxDU",
				"gap": 6.705722791630592,
				"focus": 0.07473002159827266
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					2.3833847967959514,
					56.778139023048595
				]
			]
		},
		{
			"type": "rectangle",
			"version": 163,
			"versionNonce": 1610539928,
			"index": "b00",
			"isDeleted": false,
			"id": "cQ_KmXjkQUT2X2IrrtphT",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 430.85077748384106,
			"y": 29.329366850886572,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 205.00352534413787,
			"height": 91.00623788641644,
			"seed": 857748200,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "YgGcNJtz"
				},
				{
					"id": "e4IQVChojtLh2KDXvDU9Y",
					"type": "arrow"
				}
			],
			"updated": 1716362024997,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 84,
			"versionNonce": 533721576,
			"index": "b01",
			"isDeleted": false,
			"id": "YgGcNJtz",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 449.48263659145687,
			"y": 37.332485794094794,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 167.73980712890625,
			"height": 75,
			"seed": 1011058664,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716362030568,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "When user looking\nfor a change\nroute here",
			"rawText": "When user looking for a change\nroute here",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "cQ_KmXjkQUT2X2IrrtphT",
			"originalText": "When user looking for a change\nroute here",
			"lineHeight": 1.25
		},
		{
			"type": "arrow",
			"version": 52,
			"versionNonce": 1997868895,
			"index": "b02",
			"isDeleted": false,
			"id": "e4IQVChojtLh2KDXvDU9Y",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 269.9134304847048,
			"y": 20.70772326164729,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 153.27366380870126,
			"height": 34.486574356957824,
			"seed": 2119267224,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710723,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "cQ_KmXjkQUT2X2IrrtphT",
				"gap": 7.663683190434995,
				"focus": -0.0750960530911654
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					153.27366380870126,
					34.486574356957824
				]
			]
		},
		{
			"type": "arrow",
			"version": 47,
			"versionNonce": 1769580831,
			"index": "b03",
			"isDeleted": false,
			"id": "X2ZQWzcOifTeUfO6UqfE6",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 114.15441365669852,
			"y": -86.0109161755806,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 126.68320032475825,
			"height": 0.989712502537202,
			"seed": 717258533,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710719,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 5.669960438131056,
				"focus": -0.29136090530733916
			},
			"endBinding": {
				"elementId": "SbZBXt0NSX62yD8wtwetN",
				"gap": 7.206523428874689,
				"focus": 0.5368811325989834
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-126.68320032475825,
					-0.989712502537202
				]
			]
		},
		{
			"type": "arrow",
			"version": 38,
			"versionNonce": 1309017567,
			"index": "b04",
			"isDeleted": false,
			"id": "cLdn3CjIWMg9TWhsw2MT9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 409.0645715910564,
			"y": -80.07308923587512,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 114.8037243304833,
			"height": 2.9690618361331502,
			"seed": 1783938027,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1716522710720,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "poykHqfjjrin83MrbeBy3",
				"gap": 6.602202170846724,
				"focus": -0.3269849294528686
			},
			"endBinding": {
				"elementId": "zSZ8Pfb09edupUhY2nAG5",
				"gap": 11.875414809751561,
				"focus": 0.2897648109350589
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-114.8037243304833,
					-2.9690618361331502
				]
			]
		},
		{
			"type": "rectangle",
			"version": 117,
			"versionNonce": 641878667,
			"index": "b05",
			"isDeleted": false,
			"id": "ceg7ubbu43-MfxgHvHm9u",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 659.4383716486853,
			"y": -347.76839093310554,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 572.005924418566,
			"height": 566.1968233626723,
			"seed": 82122853,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1716367635814,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 316,
			"versionNonce": 916356235,
			"index": "b09",
			"isDeleted": false,
			"id": "uZGW3Jsy",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 678.3271266085021,
			"y": 49.62689517722595,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 331.91961669921875,
			"height": 100,
			"seed": 1895375013,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716367644910,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Reference\n1. Human in the loop\n2. Persistence\n3. Basic Multiagent Collaboration",
			"rawText": "Reference\n1. Human in the loop\n2. Persistence\n3. Basic Multiagent Collaboration",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Reference\n1. Human in the loop\n2. Persistence\n3. Basic Multiagent Collaboration",
			"lineHeight": 1.25
		},
		{
			"type": "text",
			"version": 508,
			"versionNonce": 347231845,
			"index": "b0B",
			"isDeleted": false,
			"id": "fbGfUmj1",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 673.5652218465975,
			"y": -309.420723870393,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 536.2193603515625,
			"height": 325,
			"seed": 2036314379,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716367647610,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Instructions:\n1. Use google gemini 1.5\n2. Use langsmit for tracking\n3. Use sql file (not memory) to session persistence\n4. For JD, create sql db populate values, table\n    - name\n    - id\n    - designation\n    - skills\n    - years of exp\n\n5. JD Tool should access the data from this new JD\ndatabase",
			"rawText": "Instructions:\n1. Use google gemini 1.5\n2. Use langsmit for tracking\n3. Use sql file (not memory) to session persistence\n4. For JD, create sql db populate values, table\n    - name\n    - id\n    - designation\n    - skills\n    - years of exp\n\n5. JD Tool should access the data from this new JD\ndatabase",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Instructions:\n1. Use google gemini 1.5\n2. Use langsmit for tracking\n3. Use sql file (not memory) to session persistence\n4. For JD, create sql db populate values, table\n    - name\n    - id\n    - designation\n    - skills\n    - years of exp\n\n5. JD Tool should access the data from this new JD\ndatabase",
			"lineHeight": 1.25
		},
		{
			"type": "freedraw",
			"version": 5,
			"versionNonce": 1877982239,
			"index": "b0A",
			"isDeleted": true,
			"id": "Gck7IR8ABbavbFXm4f39N",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 671.6604599418356,
			"y": -409.420723870393,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 0.0001,
			"height": 0.0001,
			"seed": 1740469157,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1716528338785,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.0001,
					0.0001
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		}
	],
	"appState": {
		"theme": "dark",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 1,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 20,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 623.1014448200692,
		"scrollY": 539.8698311777084,
		"zoom": {
			"value": 1
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		},
		"objectsSnapModeEnabled": false
	},
	"files": {}
}
```
%%