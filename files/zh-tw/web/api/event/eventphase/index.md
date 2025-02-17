---
title: Event.eventPhase
slug: Web/API/Event/eventPhase
---
{{ApiRef("DOM")}}

表示事件物件目前於事件流（Event Flow）中傳遞的進度為哪一個階段。

## 語法

```js
var phase = event.eventPhase;
```

回傳一個整數值以代表目前事件於事件流中的傳遞階段，可能的值將於[事件傳遞階段常數](#事件傳遞階段常數)說明。

## 常數

### 事件傳遞階段常數

These values describe which phase the event flow is currently being evaluated.

| 常數                                                                      | 值  | 說明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------- | --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {{domxref("Event.NONE")}} {{readonlyinline}}                 | 0   | No event is being processed at this time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| {{domxref("Event.CAPTURING_PHASE")}} {{readonlyinline}} | 1   | The event is being propagated through the target's ancestor objects. This process starts with the {{domxref("Window")}}, then {{domxref("Document")}}, then the {{domxref("HTMLHtmlElement")}}, and so on through the elements until the target's parent is reached. {{domxref("EventListener", "Event listeners", "", 1)}} registered for capture mode when {{domxref("EventTarget.addEventListener()")}} was called are triggered during this phase. |
| {{domxref("Event.AT_TARGET")}} {{readonlyinline}}         | 2   | The event has arrived at {{domxref("EventTarget", "the event's target", "", 1)}}. Event listeners registered for this phase are called at this time. If {{domxref("Event.bubbles")}} is false, processing the event is finished after this phase is complete.                                                                                                                                                                                                                            |
| {{domxref("Event.BUBBLING_PHASE")}} {{readonlyinline}} | 3   | The event is propagating back up through the target's ancestors in reverse order, starting with the parent, and eventually reaching the containing {{domxref("Window")}}. This is known as bubbling, and occurs only if {{domxref("Event.bubbles")}} is `true`. {{domxref("EventListener", "Event listeners", "", 1)}} registered for this phase are triggered during this process.                                                                                              |

For more details, see [section 3.1, Event dispatch and DOM event flow](http://www.w3.org/TR/DOM-Level-3-Events/#event-flow), of the DOM Level 3 Events specification.

## 範例

### HTML Content

```html
<h4>Event Propagation Chain</h4>
<ul>
  <li>Click 'd1'</li>
  <li>Analyse event propagation chain</li>
  <li>Click next div and repeat the experience</li>
  <li>Change Capturing mode</li>
  <li>Repeat the experience</li>
</ul>
<input type="checkbox" id="chCapture" />
<label for="chCapture">Use Capturing</label>
 <div id="d1">d1
  <div id="d2">d2
      <div id="d3">d3
          <div id="d4">d4</div>
      </div>
  </div>
 </div>
 <div id="divInfo"></div>
```

### CSS Content

```css
div {
  margin: 20px;
  padding: 4px;
  border: thin black solid;
}

#divInfo {
  margin: 18px;
  padding: 8px;
  background-color:white;
  font-size:80%;
}
```

### JavaScript Content

```js
var clear = false, divInfo = null, divs = null, useCapture = false;
window.onload = function () {
  divInfo = document.getElementById("divInfo");
  divs = document.getElementsByTagName('div');
  chCapture = document.getElementById("chCapture");
  chCapture.onclick = function () {
    RemoveListeners();
    AddListeners();
  }
  Clear();
  AddListeners();
}

function RemoveListeners() {
  for (var i = 0; i < divs.length; i++) {
    var d = divs[i];
    if (d.id != "divInfo") {
      d.removeEventListener("click", OnDivClick, true);
      d.removeEventListener("click", OnDivClick, false);
    }
  }
}

function AddListeners() {
  for (var i = 0; i < divs.length; i++) {
    var d = divs[i];
    if (d.id != "divInfo") {
      d.addEventListener("click", OnDivClick, false);
      if (chCapture.checked)
        d.addEventListener("click", OnDivClick, true);
      d.onmousemove = function () { clear = true; };
    }
  }
}

function OnDivClick(e) {
  if (clear) {
    Clear(); clear = false;
  }
  if (e.eventPhase == 2)
    e.currentTarget.style.backgroundColor = 'red';
  var level = e.eventPhase == 0 ? "none" : e.eventPhase == 1 ? "capturing" : e.eventPhase == 2 ? "target" : e.eventPhase == 3 ? "bubbling" : "error";
  divInfo.innerHTML += e.currentTarget.id + "; eventPhase: " + level + "<br/>";
}

function Clear() {
  for (var i = 0; i < divs.length; i++) {
    if (divs[i].id != "divInfo")
      divs[i].style.backgroundColor = (i & 1) ? "#f6eedb" : "#cceeff";
  }
  divInfo.innerHTML = '';
}
```

{{ EmbedLiveSample('Example', '', '700', '', 'Web/API/Event/eventPhase') }}

## 規範

{{Specifications}}
