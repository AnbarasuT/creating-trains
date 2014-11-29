var pageContainer, menuContainer, page0, table, nav,formContainer,vkeyCont,tableContainer,hideContainer,page01;
var pageNo=0;
var totalPages=1;
var pageDetails=[];
var carSize=['184','133','164','201'];
var numKeypad;
var leftPos=160;
var eventType = "click";
var disabled=$("vKeyPad").droppable("disable");
var activityName="imth-6-5-4-2-1-creatingtrains";
var tableBlock;
$(document).ready(function(){
        pageContainer = $('<div id="interactive-container"></div>');
        menuContainer = $('<div id="page-container"></div>');
        page0 = $('<div id="page-0" class="page"></div>');
        table=['<div id="blocker" onclick="instruct()" ></div><div class="question" onclick="instruct()"><div style="position:absolute; left:2%; top:6%; opacity:0.6;" ><div><img src="images/btInfoOn.png" width="30px" height="30px" /></div></div><span style="text-align:left; font-family:myFontfamily; left:50px; line-height:1.4em; width:490px; position:absolute; top:45px;">Create trains by attaching compartments to the locomotive. Tap on the Table button to see information about each compartment. Write the equation matching your train(s) in the yellow area below the train. If your train is long, scroll the tracks by swiping the green area below the train track. Tap on the New Train button to create new train designs.</span><i style="font-size: 28px;  float:right; opacity: .6;" class="closeBtn icon icon-emove" ><strong>&times;</strong></i></div>'];
	
	tableBlock = $("<div id=\"tabBlock\"></div>");
	
        nav = $('<div class="contentHolder"><div class="container"><div class="contentFeedback"><div id=\"prev\"></div><div id=\"updatePage\"><span id=\"tno\" class=\"upValue\">1</span><span> of </span><span id=\"pno\" class=\"upValue\">1</span></div><div id=\"next\"></div><div id=\"del\" ></div><div class=\"nav\"><div class="btReset" ><div class="icoReset"></div></div><div class="btInfo" onclick="openInst()" ><div class="icoInfo"></div></div><div class="btFeedback"><div class="icoFeed inactive" id="submit"></div></div></div><div class="score"><div id="contCorrect"><span id="crt">0</span> <img src="images/IconCorrect.png"></div><div id="contIncorrect"><span id="incrt">0</span><img src="images/IconIncorrect.png"></div></div></div></div></div>');
	variablename = $('<div id="idName"><div></div></div>');
	nameTxt=$("<div class=\"nameTxt\"><input class=\"inTxt\" type=\"text\" placeholder=\"Student&#39;s Name\" /></div>")
	formContainer =$('<div id="divForm"><div class=\"button_Box\"><span class=\"addicon\"></span><span style=\"position:absolute;top:8px;left:70px;line-height:20px;color:#FFF380;font-weight:normal;\">New<br/> Train</span></div><div class="showtable">Table</div><div class="topArea"><div class="draggableContainer"><div class="dragObj car1" id="car4"></div><div class="dragObj car2" id="car3"></div><div class="dragObj car3" id="car2"></div><div class="dragObj car4" id="car1"></div></div></div><div></div></div>');
	var page01 = $('<div id="page01" class="newPage" style="display: block;"><div id="droppableArea1Wrapper" class="area"><div id="droppableArea"><div class="locomotiveDiv car0"></div></div></div><div class="scrlLeft"><div class="innerLeftscr scrollButton"></div></div><div class="trackarea"></div><div class="bottomArea"><div id="textContent"><div  class="numTxt" id=\"wrap\"></div></div></div></div>')
	vkeyCont = $("<div id=\"vkeyCont\" /><div id=\"vkeyContainment\" />");
	tableContainer = $('<div id="tablediv"><div id="closeBtn"></div><table border="2"><tr style="background-color:#ffc082"><td id="td1">Name of Car</td><td id="td2">Picture of Car</td><td id="td3" style="width:18%;line-height:20px; ">Letter that Represents Car\'s Length</td><td id="td4">Length of Car</td></tr><tr><td>locomotive</td><td  style="height:25%; width:25%;padding-top:0px;"><div id="train1"></div></td><td><i>a</i></td><td>70 feet </td></tr><tr></tr><tr><td>flatcar</td><td  style="height:25%; width:25%"><div id="train2"></div></td><td><i>b</i></td><td>75 feet</td></tr><tr><td>boxcar</td><td  style="height:25%; width:18%"><div id="train3"></div></td><td><i>c</i></td><td>55 feet</td></tr><tr><td>tank car</td><td  style="height:25%; width:18%"><div id="train4"></div></td><td><i>d</i></td><td>50 feet</td></tr><tr><td>caboose</td><td  style="height:25%; width:18%"><div id="train5"></div></td><td><i>e</i></td><td>80 feet</td></tr></table></div>');
	saveContainer = $('<div id="modal-container" class="save"><div class="modal-lightbox"></div><div class="modal-wrapper"><div class="modal"><div class="modal-message"></div><div class="modal-header"></div><div class="modal-body"><h3>Are you sure you want to delete this train?</h3><div class="button-container"><div class="button save-state-button"><button  onclick=\"ok();\" style="width:75px;height:33px;font-size: 100%;font-family:GillSansInfant">Yes</button></div></div><div class="button-container"><div class="button cancel-button"><button onclick=\"cancel();\" style="width:75px;height:33px;font-size: 100%;font-family:GillSansInfant">No</button></div></div></div><div class="modal-footer"></div></div></div></div>');
	
	menuContainer.append(page0);
	formContainer.append("<div id=\"middle\"></div>");
	pageContainer.append(vkeyCont);
        pageContainer.append(menuContainer);
        $('body').append(table[0]);
	page0.append(nav);
	page0.append(variablename);
	page0.append(formContainer);
	formContainer.append(page01);
	pageContainer.append(tableContainer);
        $('body').append(pageContainer).append(tableBlock);
	var a=formContainer.html().split("</div></div></div>").splice(1,1);
	page={"pageNo":pageNo+1,"carsOrder":[],"eq":"","left":""};
	pageDetails[pageNo]=page;
	
	$('.button_Box').bind('click',function(e){
		$("#tablediv").hide();
		$("#closeBtn").hide();
		$('#tabBlock').hide();
		$('.numTxt').html('');
		$("#droppableArea").removeAttr("style");
		$('#droppableArea').children().remove();
		page={"pageNo":pageNo+1,"carsOrder":[],"eq":"","left":""};
		pageDetails.push(page);
		totalPages=pageDetails.length;
		pageNo=totalPages-1;
		setPage();
		$("#droppableArea").droppable("option", "disabled", false);
		resetEnable();
		onTriggerChange();
		$("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
	});
	
	$('#next').bind('click',function(e){
		if($('#next').css('opacity') == "1"){
			$("#tablediv").hide();
			$("#closeBtn").hide();
			$('#tabBlock').hide();
		}
		if (pageNo<totalPages-1)pageNo++;
		else return;
		$('.numTxt').html('');
		setPage();
		loadTrain();
		resetEnable();
		onTriggerChange();
		if(pageDetails[pageNo].carsOrder.length == 0) $("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
	});
	
	$('#prev').bind('click',function(e){
		if($('#prev').css('opacity') == "1"){
			$("#tablediv").hide();
			$("#closeBtn").hide();
			$('#tabBlock').hide();
		}
		if (pageNo>0)pageNo--;
		else return;
		$('.numTxt').html('');
		setPage();
		loadTrain();
		resetEnable();
		onTriggerChange();
		if(pageDetails[pageNo].carsOrder.length == 0) $("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
	});
      
    	$('#del').click(function(){
		if($("#del").css("opacity") == 1) removeElement();
	
	});
	
	numKeypad = new vKeyPad(".numTxt", "#vkeyCont", {colCount: 5,
			keys:["1","2","3","4","5",
			      "6","7","8","9","0",
			      {"id":"a", "innerHTML":"<i>a</i>", "value":"a", "isSpecialKey":true, "rowIndex":3, "colSpan":1, callback:alphaKeysCallBack},
			      {"id":"b", "innerHTML":"<i>b</i>", "value":"b", "isSpecialKey":true, "rowIndex":3, "colSpan":1, callback:alphaKeysCallBack},
			      {"id":"c", "innerHTML":"<i>c</i>", "value":"c", "isSpecialKey":true, "rowIndex":3, "colSpan":1, callback:alphaKeysCallBack},
			      {"id":"d", "innerHTML":"<i>d</i>", "value":"d", "isSpecialKey":true, "rowIndex":3, "colSpan":1, callback:alphaKeysCallBack},
			      {"id":"e", "innerHTML":"<i>e</i>", "value":"e", "isSpecialKey":true, "rowIndex":3, "colSpan":1, callback:alphaKeysCallBack},
			      {"id":"plus", "innerHTML":"+", "value":"<span class=\"vDelByTag\"> &plus; </span>", "isSpecialKey":false, "rowIndex":4, "colSpan":1},"(",")",
			      {"id":"multi", "innerHTML":"&#x000D7;", "value":"<span class=\"vDelByTag\"> &#x000D7; </span>", "isSpecialKey":false, "rowIndex":4, "colSpan":1},
			      {"id":"equal", "innerHTML":"=", "value":"<span class=\"vDelByTag\"> = </span>", "isSpecialKey":false, "rowIndex":4, "colSpan":1},     
			],
			useComplexMath:false,
			useParseMath:false, deleteMethod:"byChar", clearZero:false, isForceTaggable:true,
			isMultiline:true,
			maximumLength:127
	});
	
	$(".showtable").click(function(){
		//resetEnable();
		$(".icoReset").css({'opacity':'1','cursor':'pointer'});
		$("#tablediv").show();
		$("#closeBtn").show();
		$('#tabBlock').show();
		$("#closeBtn").click(function(){	
			$("#tablediv").hide();
			$('#tabBlock').hide();
		});
	});
		
	numKeypad.onTextChanged=function(event,vk){
		pageDetails[pageNo].eq=$(vk.CurrentFocus).html();
		resetEnable();
	};
	
	$(".icoReset").css({'opacity':'0.5'});
		//$("body").css({"-webkit-transform":"scale(1)"});
		eventBroker.publishEvent("#fetch", { type : 'state' }, function(state) {
		    if(state){
			var savedState = JSON.parse(state);
			if(savedState["activityName"] == activityName)
			    _.each(savedState, function(value, key, list) {
					if(key == "pageNo")pageNo=value;
					if(key == "pageDetails")pageDetails=value;
					else if (key=="visitedPage") {
					    $('totalPages').html(value);
					}
				});
				setPage();
				loadTrain();
				resetEnable();
				onTriggerChange();
				if(pageDetails[pageNo].carsOrder.length == 0) $("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
			}
		});
		
	setTimeout(function(){
		$("body").css({"-webkit-transform":"scale(1)"});
	}, 1000);
	
	$(".icoReset").bind(eventType,resetOnClick);
	
	var draggableObject = new Drag($(".scrollButton"), {axis:"x"});
	draggableObject.OnDrag = function(){
		if(draggableObject.touchedElement) setScrollerProp(draggableObject.touchedElement, true);
	}
	
	dragEnable();
	dropEnable();
	setPage();
	onTriggerChange();
});

function loadTrain() {
		$("#droppableArea").children().remove();
		for (var i=0;i<pageDetails[pageNo].carsOrder.length;i++){
			car=$("<div class=\"car"+pageDetails[pageNo].carsOrder[i]+"\"></div>");
			car.css({position:'relative',height:"53px",width:"240px"}).addClass('dupObj');
			$("#droppableArea").append(car);
		}
		dropEnable();
		dragEnable();
		width=$("#droppableArea").width();	
		$('.numTxt').html(pageDetails[pageNo].eq);
		onTriggerChange();
}

function setPage() {
	$("#tno").html(pageNo+1);
	$("#pno").html(pageDetails.length);
	totalPages=pageDetails.length;
	if (pageNo>0) $('#prev').css('opacity','1');
	else $('#prev').css('opacity','0.5');
	if (totalPages>1){
		$('#del').css('opacity','1');
		resetEnable();
        }
        else{
		$('#del').css('opacity','0.5');
		resetEnable();
        }	
	if(pageNo<totalPages-1) $('#next').css('opacity','1');
	else $('#next').css('opacity','0.5');
	onTriggerChange();
}

function alphaKeysCallBack(keyPad, existingText, keyDetails){
	return existingText+"<i>"+keyDetails.value+"</i>";
}

function instruct(){
	$('.question,#blocker').hide();
	$('.btInfo').css({'opacity':'1','cursor':'pointer'});
	try {
		$('#instructions-button-container').unbind('click',openInst);
	} catch(e){}
		$('#instructions-button-container').bind('click',openInst);
}

function openInst(){
	$('.question,#blocker').show();
	$('.btInfo').css({'opacity':'0.5'});
}

function toggleClassButton(element,className){
	var currentButton=element;
	if(!currentButton.hasClass(className)){
		currentButton.addClass(className);
	}
	else{
		currentButton.removeClass(className);	
	}
}

function dragEnable() {
	dropCount = 0;
	$('.car0').removeClass('ui-draggable');
	$(".car0").draggable({ disabled: true });
	$(".dragObj").draggable({
		containment:"#divForm",
		stack:".dragObj",
		zIndex:100000,
		helper: "clone"
	});
	
	$("#tablediv").draggable({
		containment:'#vkeyContainment'
	});
	
	$(".dupObj").draggable({
				stack: ".dupObj" ,
				revert : function(event, ui) {
				var canRemove=removeItem($(this));
				
				if (canRemove) {
					$(this).remove();
					$("#droppableArea").droppable("option", "disabled", false);
					updateCarsOrder();
					onTriggerChange();
				}else
				{
				$(this).data("uiDraggable").originalPosition = {
					top : 55,
					left : 0
				};
				}
					return !event;
				}
			});
}

function dropEnable(){
	$("#droppableArea").droppable({
		zIndex:100000,
		items:"div:not(.car0)",
		containment:"#divForm",
		drop:function(e,ui){
			//css({position:'relative',height:"53px",width:"240"})
			$(this).append($(ui.draggable).clone().removeAttr('style').removeAttr('id').removeClass("dragObj").addClass("dupObj"));//.addClass("dubObj"));
			//if ($("#droppableArea").children().length>=100)
			//{
			//	$("#droppableArea").droppable("option", "disabled", true);
			//}
			onTriggerChange();
			updateCarsOrder();
			resetEnable();
			
		$(".dupObj").draggable({
				stack: ".dupObj" ,
				revert : function(event, ui) {
				var canRemove=removeItem($(this));
				
				if (canRemove) {
					$(this).remove();
					$("#droppableArea").droppable("option", "disabled", false);
					updateCarsOrder();
					onTriggerChange();
				}
				else
				{
					$(this).data("uiDraggable").originalPosition = {
						top : 55,
						left : 0
					};
				}
					return !event;
				}
			});	
		},
		accept:'.dragObj'
	});
}


function removeItem(item) {
	left=$("#droppableArea1Wrapper").position().left;
	topC=$("#droppableArea1Wrapper").position().top;
	width=$("#droppableArea1Wrapper").width();
	height=$("#droppableArea1Wrapper").height();
	//item.position().top < -55 && item.position().top >156 
	//if (item.position().top > ($("#droppableArea1Wrapper").position().top+height-adjustment))
	if (item.position().top < -55 || item.position().top >156) return true;
	else return false; 
}

function updateCarsOrder() {
	page={"pageNo":pageNo+1,"carsOrder":[],"eq":"","left":""};
	page.eq=$('.numTxt').html();
	pageInfo=[];
	posleft=$("#droppableArea").position().left;
	$("#droppableArea").children().each(function(){
		var img=$(this).css("background-image").substr($(this).css("background-image").lastIndexOf('.')-1,1);
		pageInfo.push(img);
	});
	page.carsOrder=pageInfo;
	pageDetails[pageNo]=page;
	page.left=posleft;
	onTriggerChange();
}

function  resetEnable() {
	if ($('#droppableArea').children().length>1 || $('.numTxt').html()!="") {		
		$(".icoReset").css({'opacity':'1','cursor':'pointer'});
		//$("#del").css({'opacity':'1'});
	}
	else
	{
	      $(".icoReset").css({'opacity':'0.5','cursor':'pointer'});
	       // $("#del").css({'opacity':'0.5'});
	}
}

function resetOnClick() {
	if ($('.icoReset').css('opacity') == "1") {
		$(".icoReset").removeClass('icoResetMove');
		var to=setTimeout(function(){
		clearInterval(to);
		$(".icoReset").addClass('icoResetMove');
		$('.icoReset').css({'opacity':'0.5','cursor':'default'});
		},200);
		$("#tablediv").hide();
		pageDetails[pageNo].eq="";
		pageDetails[pageNo].carsOrder=[];
		pageDetails[pageNo].pageNo=0;
		pageDetails[pageNo].left="";
		loadTrain();
		$('#tabBlock').hide();
		dragEnable();
		if(pageDetails[pageNo].carsOrder.length == 0) $("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
	}
}
 
function removeElement() {
	$("#tablediv").hide();
	$("#closeBtn").hide();
	$('#tabBlock').hide();
	$("#interactive-container").append(saveContainer);
	onTriggerChange();
}

function ok(){
	deleteElement();
	$("#modal-container").remove();
	onTriggerChange();
}

function cancel(){
    $("#modal-container").remove();
    onTriggerChange();
}

function deleteElement(){
	pageDetails.splice(pageNo,1);
	if (pageNo!=0)pageNo--;
	loadTrain();
	setPage();
	onTriggerChange();
	if(pageDetails[pageNo].carsOrder.length == 0) $("#droppableArea").append("<div class=\"locomotiveDiv car0\"></div>");
}

	eventBroker = _({}).extend(require('chaplin/lib/event_broker'));
	eventBroker.subscribeEvent('#doSave', function(state) {
	    var state = {};
	    state = {"pageDetails":pageDetails,"activityName":activityName,"pageNo":pageNo,"visitedPage":totalPages};
		var message = {
		    type : 'state',
		    data : JSON.stringify(state)
	    };
	    eventBroker.publishEvent("#save", message);
	});

function saveFunction(){
	eventBroker.publishEvent("#doSave");
}
 
function onTriggerChange() {
	scrollbar();
	setScrollerProp($(".innerLeftscr"));
}

function scrollbar(){
	var dropCount=droppableArea.children.length;
	var eachLeft=$("#droppableArea").position().left;
	var totalWidthReq =162;//= dropCount*240;
	for (var i=1;i<pageDetails[pageNo].carsOrder.length;i++) {
	      totalWidthReq+=parseInt(carSize[pageDetails[pageNo].carsOrder[i]-1]);
	}
	var minWidthReq = $("#droppableArea1Wrapper").width();
	var widthToApply = Math.max(minWidthReq, totalWidthReq);
	$("#droppableArea").css({"width":widthToApply+"px", "left":(minWidthReq-widthToApply)+"px"});
}

function setScrollerProp(scrollButton,isScrollChange) {
	try{
		var scrollbar = scrollButton.parent();
		var referenceArea = scrollbar.parent().find(".area");
		var innerArea = referenceArea.children().eq(0);
		if (innerArea.width() > referenceArea.outerWidth(true)) {
		    var hiddenArea = innerArea.width() - referenceArea.outerWidth(true);
		    var scrollBtnMaxLeft = scrollbar.width()-scrollButton.outerWidth(true);
		    var posPerc = (parseFloat(scrollButton.css("left").replace("px","")))/scrollBtnMaxLeft;
		    if (isNaN(posPerc) || !isFinite(posPerc)) posPerc = 0;
			scrollButton.clearQueue();
			var visiblePerc = referenceArea.outerWidth(true)/innerArea.width();
			var proposedWidth = visiblePerc*scrollbar.width();
			scrollBtnMaxLeft = scrollbar.width()-proposedWidth;
			if (!isScrollChange) posPerc = 1;
			var scrollLeft = scrollBtnMaxLeft*posPerc;
			if (!isScrollChange) scrollButton.css({"left":scrollLeft+"px"});
			var topAdj = (scrollButton.position().left+proposedWidth) - scrollbar.width();
			if (topAdj > 0) {
			    var newLeft = scrollButton.position().left-topAdj;
			    scrollButton.css({"left":newLeft+"px"});
			}
			var left = scrollButton.position().left;
			scrollButton.css({"width":proposedWidth+"px"}, 100);
			var posPerc = left/scrollBtnMaxLeft;
			innerArea.css({"left":-(hiddenArea*posPerc)+"px"});
			if (visiblePerc >= 1) scrollButton.css({"opacity":0},100);
			else scrollButton.css({"opacity":1},100);
		}
		else {
		    scrollButton.css({"opacity":"0"});
		}
	}
	catch(e){}
}
