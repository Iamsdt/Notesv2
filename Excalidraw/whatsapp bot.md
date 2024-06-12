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
			"version": 108,
			"versionNonce": 1090398548,
			"index": "aR",
			"isDeleted": false,
			"id": "oALaHVG8uq6l1K_hm_nlS",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 81.26368083180108,
			"y": -282.52191946307,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 93.39226363954629,
			"height": 76.84115896489425,
			"seed": 946977432,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1717998121332,
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
					-93.39226363954629,
					76.84115896489425
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
			"version": 81,
			"versionNonce": 243588948,
			"index": "aX",
			"isDeleted": false,
			"id": "QFxfquLveZ81mOf5ujFMz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 6.351838438534088,
			"y": -118.62692415475513,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 88.30071474603467,
			"height": 1.8812863105228672,
			"seed": 919737832,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1717998121333,
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
					88.30071474603467,
					1.8812863105228672
				]
			]
		},
		{
			"type": "arrow",
			"version": 83,
			"versionNonce": 1780333652,
			"index": "aY",
			"isDeleted": false,
			"id": "_43zeu_EemyuubRTWGVVR",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 300.49755387389854,
			"y": -116.05249778987135,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 98.68540103123905,
			"height": 4.39768085593721,
			"seed": 405622760,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1717998121334,
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
					98.68540103123905,
					4.39768085593721
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
			"version": 184,
			"versionNonce": 1573057108,
			"index": "ac",
			"isDeleted": false,
			"id": "DgBIgKwKt-2l29TD2P_8M",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 236.21163418044603,
			"y": -20.873123076027113,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 55.7769277207143,
			"height": 100.5771452110109,
			"seed": 1206910616,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1717998121334,
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
					55.7769277207143,
					100.5771452110109
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
			"version": 81,
			"versionNonce": 2072079700,
			"index": "af",
			"isDeleted": false,
			"id": "c3GuxR7vGcvjO1uQqFjwg",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 146.32841429213087,
			"y": -36.58684163264509,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 34.10535296016586,
			"height": 112.39930554007847,
			"seed": 925048040,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1717998121335,
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
					-34.10535296016586,
					112.39930554007847
				]
			]
		},
		{
			"type": "arrow",
			"version": 44,
			"versionNonce": 1914513492,
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
			"updated": 1717998121335,
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
			"version": 46,
			"versionNonce": 457581396,
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
			"updated": 1717998121335,
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
			"version": 62,
			"versionNonce": 615276116,
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
			"updated": 1717998121336,
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
			"version": 203,
			"versionNonce": 854674260,
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
			"updated": 1717998121333,
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
			"version": 51,
			"versionNonce": 1572172756,
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
			"updated": 1717998121336,
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
			"version": 53,
			"versionNonce": 268425556,
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
			"updated": 1717998121336,
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
			"version": 51,
			"versionNonce": 1504544340,
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
			"updated": 1717998121333,
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
			"version": 42,
			"versionNonce": 322025300,
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
			"updated": 1717998121334,
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
			"id": "GUSwwOamlT0DdZfS7VXHc",
			"type": "freedraw",
			"x": -304.1340250309089,
			"y": -48.58962058802024,
			"width": 15.943804808821426,
			"height": 16.442048709097094,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"index": "b0C",
			"roundness": null,
			"seed": 652316372,
			"version": 16,
			"versionNonce": 1684622292,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1717998132196,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.9929756011026711,
					4.48419510248101
				],
				[
					2.491219501378339,
					5.480682903032346
				],
				[
					3.4877073019296745,
					4.982439002756678
				],
				[
					4.484195102481067,
					3.4877073019296745
				],
				[
					5.4806829030324025,
					2.491219501378339
				],
				[
					8.968390204962077,
					-3.4877073019296745
				],
				[
					11.459609706340416,
					-6.477170703583738
				],
				[
					12.95434140716742,
					-7.971902404410741
				],
				[
					13.950829207718755,
					-8.968390204962077
				],
				[
					14.449073107994423,
					-9.466634105237745
				],
				[
					14.94731700827009,
					-10.46312190578908
				],
				[
					15.943804808821426,
					-10.961365806064748
				],
				[
					15.943804808821426,
					-10.961365806064748
				]
			],
			"pressures": [],
			"simulatePressure": true,
			"lastCommittedPoint": [
				15.943804808821426,
				-10.961365806064748
			]
		},
		{
			"id": "z55go7oQUcCSBBj_XWpg2",
			"type": "freedraw",
			"x": -333.5304151471734,
			"y": -149.7331323439812,
			"width": 19.929756011026825,
			"height": 10.96136580606472,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"index": "b0D",
			"roundness": null,
			"seed": 1134869996,
			"version": 21,
			"versionNonce": 1091280236,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1717998135181,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					1.4947317008270034,
					1.4947317008270034
				],
				[
					1.9929756011026711,
					2.491219501378339
				],
				[
					2.491219501378339,
					3.4877073019296745
				],
				[
					2.9894634016540067,
					3.9859512022053423
				],
				[
					3.4877073019296745,
					3.9859512022053423
				],
				[
					4.484195102481067,
					3.9859512022053423
				],
				[
					6.477170703583738,
					2.9894634016540067
				],
				[
					8.47014630468641,
					1.4947317008270034
				],
				[
					10.46312190578908,
					-0.4982439002756678
				],
				[
					12.456097506891751,
					-1.4947317008270318
				],
				[
					13.950829207718755,
					-3.487707301929703
				],
				[
					16.442048709097094,
					-4.982439002756706
				],
				[
					17.936780409924097,
					-5.978926803308042
				],
				[
					18.435024310199765,
					-6.47717070358371
				],
				[
					18.93326821047549,
					-6.975414603859377
				],
				[
					19.431512110751157,
					-6.975414603859377
				],
				[
					19.929756011026825,
					-6.975414603859377
				],
				[
					19.929756011026825,
					-6.975414603859377
				]
			],
			"pressures": [],
			"simulatePressure": true,
			"lastCommittedPoint": [
				19.929756011026825,
				-6.975414603859377
			]
		},
		{
			"id": "K9Le_996thS1f8MCq7cKg",
			"type": "freedraw",
			"x": -332.5339273466221,
			"y": -123.32620562937072,
			"width": 21.922731612129496,
			"height": 9.964878005513384,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"index": "b0E",
			"roundness": null,
			"seed": 1073558740,
			"version": 15,
			"versionNonce": 21568596,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1717998136163,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.4982439002756678,
					0.4982439002756678
				],
				[
					0.9964878005513356,
					0.9964878005513356
				],
				[
					1.4947317008270034,
					0.9964878005513356
				],
				[
					2.491219501378339,
					0.9964878005513356
				],
				[
					5.4806829030324025,
					0.4982439002756678
				],
				[
					8.968390204962077,
					-1.4947317008270034
				],
				[
					12.95434140716742,
					-3.9859512022053423
				],
				[
					15.943804808821426,
					-5.978926803308042
				],
				[
					17.43853650964843,
					-6.975414603859377
				],
				[
					19.929756011026825,
					-8.47014630468638
				],
				[
					21.922731612129496,
					-8.968390204962049
				],
				[
					21.922731612129496,
					-8.968390204962049
				]
			],
			"pressures": [],
			"simulatePressure": true,
			"lastCommittedPoint": [
				21.922731612129496,
				-8.968390204962049
			]
		},
		{
			"id": "Dtdi6lyQgCtrfLogxnkhH",
			"type": "freedraw",
			"x": -299.64982992842783,
			"y": -184.11196146300242,
			"width": 85.19970694713948,
			"height": 22.919219412680803,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"index": "b0F",
			"roundness": null,
			"seed": 762135916,
			"version": 21,
			"versionNonce": 1104696556,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1717998137923,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.4982439002756678,
					-0.9964878005513356
				],
				[
					1.9929756011026711,
					-2.989463401654035
				],
				[
					5.480682903032346,
					-7.473658504135045
				],
				[
					8.96839020496202,
					-9.466634105237745
				],
				[
					20.926243811578104,
					-16.442048709097094
				],
				[
					30.39287791681585,
					-19.929756011026797
				],
				[
					41.35424372288054,
					-22.420975512405136
				],
				[
					50.32263392784262,
					-22.919219412680803
				],
				[
					58.792780232529026,
					-22.919219412680803
				],
				[
					68.75765823804238,
					-20.926243811578132
				],
				[
					76.23131674217746,
					-17.936780409924125
				],
				[
					78.22429234328013,
					-16.94029260937279
				],
				[
					80.71551184465847,
					-14.94731700827009
				],
				[
					82.70848744576114,
					-13.452585307443087
				],
				[
					83.70497524631247,
					-12.456097506891751
				],
				[
					84.70146304686381,
					-11.459609706340416
				],
				[
					85.19970694713948,
					-10.961365806064748
				],
				[
					85.19970694713948,
					-10.961365806064748
				]
			],
			"pressures": [],
			"simulatePressure": true,
			"lastCommittedPoint": [
				85.19970694713948,
				-10.961365806064748
			]
		},
		{
			"id": "1kaPqz1th9Bk2TvP9RaCv",
			"type": "freedraw",
			"x": -219.43256198404504,
			"y": -195.07332726906716,
			"width": 26.406926714610506,
			"height": 21.922731612129468,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"index": "b0G",
			"roundness": null,
			"seed": 582329684,
			"version": 34,
			"versionNonce": 684152148,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1717998139131,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					0.4982439002756678,
					0.9964878005513356
				],
				[
					1.4947317008270034,
					1.9929756011026996
				],
				[
					2.9894634016540067,
					2.989463401654035
				],
				[
					4.982439002756678,
					4.4841951024810385
				],
				[
					7.971902404410741,
					6.47717070358371
				],
				[
					10.961365806064748,
					8.47014630468638
				],
				[
					14.449073107994423,
					9.466634105237745
				],
				[
					16.442048709097094,
					9.466634105237745
				],
				[
					17.43853650964843,
					9.466634105237745
				],
				[
					19.4315121107511,
					8.47014630468638
				],
				[
					19.929756011026825,
					4.982439002756706
				],
				[
					19.929756011026825,
					1.9929756011026996
				],
				[
					19.929756011026825,
					0.4982439002756678
				],
				[
					19.929756011026825,
					-3.4877073019296745
				],
				[
					19.929756011026825,
					-6.975414603859377
				],
				[
					19.929756011026825,
					-9.466634105237716
				],
				[
					19.929756011026825,
					-10.96136580606472
				],
				[
					19.929756011026825,
					-11.459609706340387
				],
				[
					19.929756011026825,
					-11.957853606616055
				],
				[
					19.4315121107511,
					-12.456097506891723
				],
				[
					17.43853650964843,
					-11.459609706340387
				],
				[
					16.442048709097094,
					-10.96136580606472
				],
				[
					11.459609706340416,
					-7.971902404410713
				],
				[
					7.473658504135074,
					-5.480682903032346
				],
				[
					3.4877073019296745,
					-3.9859512022053423
				],
				[
					-0.4982439002756678,
					-2.491219501378339
				],
				[
					-3.4877073019296745,
					-0.9964878005513356
				],
				[
					-4.982439002756678,
					-0.4982439002756678
				],
				[
					-5.978926803308013,
					-0.4982439002756678
				],
				[
					-6.477170703583681,
					0
				],
				[
					-6.477170703583681,
					0
				]
			],
			"pressures": [],
			"simulatePressure": true,
			"lastCommittedPoint": [
				-6.477170703583681,
				0
			]
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
		"scrollX": 703.9747550021339,
		"scrollY": 332.33173673407236,
		"zoom": {
			"value": 2.007049156942448
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