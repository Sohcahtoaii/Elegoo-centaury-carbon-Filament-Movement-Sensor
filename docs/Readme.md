<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive BOM for KiCAD</title>
  <style type="text/css">
:root {
  --pcb-edge-color: black;
  --pad-color: #878787;
  --pad-hole-color: #CCCCCC;
  --pad-color-highlight: #D04040;
  --pad-color-highlight-both: #D0D040;
  --pad-color-highlight-marked: #44a344;
  --pin1-outline-color: #ffb629;
  --pin1-outline-color-highlight: #ffb629;
  --pin1-outline-color-highlight-both: #fcbb39;
  --pin1-outline-color-highlight-marked: #fdbe41;
  --silkscreen-edge-color: #aa4;
  --silkscreen-polygon-color: #4aa;
  --silkscreen-text-color: #4aa;
  --fabrication-edge-color: #907651;
  --fabrication-polygon-color: #907651;
  --fabrication-text-color: #a27c24;
  --track-color: #def5f1;
  --track-color-highlight: #D04040;
  --zone-color: #def5f1;
  --zone-color-highlight: #d0404080;
}

html,
body {
  margin: 0px;
  height: 100%;
  font-family: Verdana, sans-serif;
}

.dark.topmostdiv {
  --pcb-edge-color: #eee;
  --pad-color: #808080;
  --pin1-outline-color: #ffa800;
  --pin1-outline-color-highlight: #ccff00;
  --track-color: #42524f;
  --zone-color: #42524f;
  background-color: #252c30;
  color: #eee;
}

button {
  background-color: #eee;
  border: 1px solid #888;
  color: black;
  height: 44px;
  width: 44px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  font-weight: bolder;
}

.dark button {
  /* This will be inverted */
  background-color: #c3b7b5;
}

button.depressed {
  background-color: #0a0;
  color: white;
}

.dark button.depressed {
  /* This will be inverted */
  background-color: #b3b;
}

button:focus {
  outline: 0;
}

button#tb-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' fill='none' stroke='%23000' stroke-width='.4' stroke-linejoin='round'/%3E%3Cpath d='M1.32 290.12h5.82M1.32 291.45h5.82' fill='none' stroke='%23000' stroke-width='.4'/%3E%3Cpath d='M4.37 292.5v4.23M.26 292.63H8.2' fill='none' stroke='%23000' stroke-width='.3'/%3E%3Ctext font-weight='700' font-size='3.17' font-family='sans-serif'%3E%3Ctspan x='1.35' y='295.73'%3EF%3C/tspan%3E%3Ctspan x='5.03' y='295.68'%3EB%3C/tspan%3E%3C/text%3E%3C/g%3E%3C/svg%3E%0A");
}

button#lr-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' fill='none' stroke='%23000' stroke-width='.4' stroke-linejoin='round'/%3E%3Cpath d='M1.06 290.12H3.7m-2.64 1.33H3.7m-2.64 1.32H3.7m-2.64 1.3H3.7m-2.64 1.33H3.7' fill='none' stroke='%23000' stroke-width='.4'/%3E%3Cpath d='M4.37 288.8v7.94m0-4.11h3.96' fill='none' stroke='%23000' stroke-width='.3'/%3E%3Ctext font-weight='700' font-size='3.17' font-family='sans-serif'%3E%3Ctspan x='5.11' y='291.96'%3EF%3C/tspan%3E%3Ctspan x='5.03' y='295.68'%3EB%3C/tspan%3E%3C/text%3E%3C/g%3E%3C/svg%3E%0A");
}

button#bom-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)' fill='none' stroke='%23000' stroke-width='.4'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' stroke-linejoin='round'/%3E%3Cpath d='M1.59 290.12h5.29M1.59 291.45h5.33M1.59 292.75h5.33M1.59 294.09h5.33M1.59 295.41h5.33'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-grouped-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg stroke='%23000' stroke-linejoin='round' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-linecap='square' stroke-width='2' d='M6 10h4m4 0h5m4 0h3M6.1 22h3m3.9 0h5m4 0h4m-16-8h4m4 0h4'/%3E%3Cpath stroke-linecap='null' d='M5 17.5h22M5 26.6h22M5 5.5h22'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-ungrouped-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg stroke='%23000' stroke-linejoin='round' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-linecap='square' stroke-width='2' d='M6 10h4m-4 8h3m-3 8h4'/%3E%3Cpath stroke-linecap='null' d='M5 13.5h22m-22 8h22M5 5.5h22'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-netlist-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg fill='none' stroke='%23000' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-width='2' d='M6 26l6-6v-8m13.8-6.3l-6 6v8'/%3E%3Ccircle cx='11.8' cy='9.5' r='2.8' stroke-width='2'/%3E%3Ccircle cx='19.8' cy='22.8' r='2.8' stroke-width='2'/%3E%3C/g%3E%3C/svg%3E");
}

button#copy {
  background-image: url("data:image/svg+xml,%3Csvg height='48' viewBox='0 0 48 48' width='48' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0 0h48v48h-48z' fill='none'/%3E%3Cpath d='M32 2h-24c-2.21 0-4 1.79-4 4v28h4v-28h24v-4zm6 8h-22c-2.21 0-4 1.79-4 4v28c0 2.21 1.79 4 4 4h22c2.21 0 4-1.79 4-4v-28c0-2.21-1.79-4-4-4zm0 32h-22v-28h22v28z'/%3E%3C/svg%3E");
  background-position: 6px 6px;
  background-repeat: no-repeat;
  background-size: 26px 26px;
  border-radius: 6px;
  height: 40px;
  width: 40px;
  margin: 10px 5px;
}

button#copy:active {
  box-shadow: inset 0px 0px 5px #6c6c6c;
}

textarea.clipboard-temp {
  position: fixed;
  top: 0;
  left: 0;
  width: 2em;
  height: 2em;
  padding: 0;
  border: None;
  outline: None;
  box-shadow: None;
  background: transparent;
}

.left-most-button {
  border-right: 0;
  border-top-left-radius: 6px;
  border-bottom-left-radius: 6px;
}

.middle-button {
  border-right: 0;
}

.right-most-button {
  border-top-right-radius: 6px;
  border-bottom-right-radius: 6px;
}

.button-container {
  font-size: 0;
  margin: 0.4rem 0.4rem 0.4rem 0;
}

.dark .button-container {
  filter: invert(1);
}

.button-container button {
  background-size: 32px 32px;
  background-position: 5px 5px;
  background-repeat: no-repeat;
}

@media print {
  .hideonprint {
    display: none;
  }
}

canvas {
  cursor: crosshair;
}

canvas:active {
  cursor: grabbing;
}

.fileinfo {
  width: 100%;
  max-width: 1000px;
  border: none;
  padding: 3px;
}

.fileinfo .title {
  font-size: 20pt;
  font-weight: bold;
}

.fileinfo td {
  overflow: hidden;
  white-space: nowrap;
  max-width: 1px;
  width: 50%;
  text-overflow: ellipsis;
}

.bom {
  border-collapse: collapse;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 10pt;
  table-layout: fixed;
  width: 100%;
  margin-top: 1px;
  position: relative;
}

.bom th,
.bom td {
  border: 1px solid black;
  padding: 5px;
  word-wrap: break-word;
  text-align: center;
  position: relative;
}

.dark .bom th,
.dark .bom td {
  border: 1px solid #777;
}

.bom th {
  background-color: #CCCCCC;
  background-clip: padding-box;
}

.dark .bom th {
  background-color: #3b4749;
}

.bom tr.highlighted:nth-child(n) {
  background-color: #cfc;
}

.dark .bom tr.highlighted:nth-child(n) {
  background-color: #226022;
}

.bom tr:nth-child(even) {
  background-color: #f2f2f2;
}

.dark .bom tr:nth-child(even) {
  background-color: #313b40;
}

.bom tr.checked {
  color: #1cb53d;
}

.dark .bom tr.checked {
  color: #2cce54;
}

.bom tr {
  transition: background-color 0.2s;
}

.bom .numCol {
  width: 30px;
}

.bom .value {
  width: 15%;
}

.bom .quantity {
  width: 65px;
}

.bom th .sortmark {
  position: absolute;
  right: 1px;
  top: 1px;
  margin-top: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent #221 transparent;
  transform-origin: 50% 85%;
  transition: opacity 0.2s, transform 0.4s;
}

.dark .bom th .sortmark {
  filter: invert(1);
}

.bom th .sortmark.none {
  opacity: 0;
}

.bom th .sortmark.desc {
  transform: rotate(180deg);
}

.bom th:hover .sortmark.none {
  opacity: 0.5;
}

.bom .bom-checkbox {
  width: 30px;
  position: relative;
  user-select: none;
  -moz-user-select: none;
}

.bom .bom-checkbox:before {
  content: "";
  position: absolute;
  border-width: 15px;
  border-style: solid;
  border-color: #51829f transparent transparent transparent;
  visibility: hidden;
  top: -15px;
}

.bom .bom-checkbox:after {
  content: "Double click to set/unset all";
  position: absolute;
  color: white;
  top: -35px;
  left: -26px;
  background: #51829f;
  padding: 5px 15px;
  border-radius: 8px;
  white-space: nowrap;
  visibility: hidden;
}

.bom .bom-checkbox:hover:before,
.bom .bom-checkbox:hover:after {
  visibility: visible;
  transition: visibility 0.2s linear 1s;
}

.split {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  overflow-y: auto;
  overflow-x: hidden;
  background-color: inherit;
}

.split.split-horizontal,
.gutter.gutter-horizontal {
  height: 100%;
  float: left;
}

.gutter {
  background-color: #ddd;
  background-repeat: no-repeat;
  background-position: 50%;
  transition: background-color 0.3s;
}

.dark .gutter {
  background-color: #777;
}

.gutter.gutter-horizontal {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAeCAYAAADkftS9AAAAIklEQVQoU2M4c+bMfxAGAgYYmwGrIIiDjrELjpo5aiZeMwF+yNnOs5KSvgAAAABJRU5ErkJggg==');
  cursor: ew-resize;
  width: 5px;
}

.gutter.gutter-vertical {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAFAQMAAABo7865AAAABlBMVEVHcEzMzMzyAv2sAAAAAXRSTlMAQObYZgAAABBJREFUeF5jOAMEEAIEEFwAn3kMwcB6I2AAAAAASUVORK5CYII=');
  cursor: ns-resize;
  height: 5px;
}

.searchbox {
  float: left;
  height: 40px;
  margin: 10px 5px;
  padding: 12px 32px;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 18px;
  box-sizing: border-box;
  border: 1px solid #888;
  border-radius: 6px;
  outline: none;
  background-color: #eee;
  transition: background-color 0.2s, border 0.2s;
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAABNklEQVQ4T8XSMUvDQBQH8P/LElFa/AIZHcTBQSz0I/gFstTBRR2KUC4ldDxw7h0Bl3RRUATxi4iiODgoiLNrbQYp5J6cpJJqomkX33Z37/14d/dIa33MzDuYI4johOI4XhyNRteO46zNYjDzAxE1yBZprVeZ+QbAUhXEGJMA2Ox2u4+fQIa0mPmsCgCgJYQ4t7lfgF0opQYAdv9ABkKI/UnOFCClXKjX61cA1osQY8x9kiRNKeV7IWA3oyhaSdP0FkAtjxhj3hzH2RBCPOf3pzqYHCilfAAX+URm9oMguPzeWSGQvUcMYC8rOBJCHBRdqxTo9/vbRHRqi8bj8XKv1xvODbiuW2u32/bvf0SlDv4XYOY7z/Mavu+nM1+BmQ+NMc0wDF/LprP0DbTWW0T00ul0nn4b7Q87+X4Qmfiq2wAAAABJRU5ErkJggg==');
  background-position: 10px 10px;
  background-repeat: no-repeat;
}

.dark .searchbox {
  background-color: #111;
  color: #eee;
}

.searchbox::placeholder {
  color: #ccc;
}

.dark .searchbox::placeholder {
  color: #666;
}

.filter {
  width: calc(60% - 64px);
}

.reflookup {
  width: calc(40% - 10px);
}

input[type=text]:focus {
  background-color: white;
  border: 1px solid #333;
}

.dark input[type=text]:focus {
  background-color: #333;
  border: 1px solid #ccc;
}

mark.highlight {
  background-color: #5050ff;
  color: #fff;
  padding: 2px;
  border-radius: 6px;
}

.dark mark.highlight {
  background-color: #76a6da;
  color: #111;
}

.menubtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 20 20'%3E%3Cpath fill='none' d='M0 0h20v20H0V0z'/%3E%3Cpath d='M15.95 10.78c.03-.25.05-.51.05-.78s-.02-.53-.06-.78l1.69-1.32c.15-.12.19-.34.1-.51l-1.6-2.77c-.1-.18-.31-.24-.49-.18l-1.99.8c-.42-.32-.86-.58-1.35-.78L12 2.34c-.03-.2-.2-.34-.4-.34H8.4c-.2 0-.36.14-.39.34l-.3 2.12c-.49.2-.94.47-1.35.78l-1.99-.8c-.18-.07-.39 0-.49.18l-1.6 2.77c-.1.18-.06.39.1.51l1.69 1.32c-.04.25-.07.52-.07.78s.02.53.06.78L2.37 12.1c-.15.12-.19.34-.1.51l1.6 2.77c.1.18.31.24.49.18l1.99-.8c.42.32.86.58 1.35.78l.3 2.12c.04.2.2.34.4.34h3.2c.2 0 .37-.14.39-.34l.3-2.12c.49-.2.94-.47 1.35-.78l1.99.8c.18.07.39 0 .49-.18l1.6-2.77c.1-.18.06-.39-.1-.51l-1.67-1.32zM10 13c-1.65 0-3-1.35-3-3s1.35-3 3-3 3 1.35 3 3-1.35 3-3 3z'/%3E%3C/svg%3E%0A");
  background-position: center;
  background-repeat: no-repeat;
}

.statsbtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg width='36' height='36' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M4 6h28v24H4V6zm0 8h28v8H4m9-16v24h10V5.8' fill='none' stroke='%23000' stroke-width='2'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
}

.iobtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36'%3E%3Cpath fill='none' stroke='%23000' stroke-width='2' d='M3 33v-7l6.8-7h16.5l6.7 7v7H3zM3.2 26H33M21 9l5-5.9 5 6h-2.5V15h-5V9H21zm-4.9 0l-5 6-5-6h2.5V3h5v6h2.5z'/%3E%3Cpath fill='none' stroke='%23000' d='M6.1 29.5H10'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
}

.visbtn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Cpath fill='none' stroke='%23333' d='M2.5 4.5h5v15h-5zM9.5 4.5h5v15h-5zM16.5 4.5h5v15h-5z'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
  padding: 15px;
}

#vismenu-content {
  left: 0px;
  font-family: Verdana, sans-serif;
}

.dark .statsbtn,
.dark .savebtn,
.dark .menubtn,
.dark .iobtn,
.dark .visbtn {
  filter: invert(1);
}

.flexbox {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.savebtn {
  background-color: #d6d6d6;
  width: auto;
  height: 30px;
  flex-grow: 1;
  margin: 5px;
  border-radius: 4px;
}

.savebtn:active {
  background-color: #0a0;
  color: white;
}

.dark .savebtn:active {
  /* This will be inverted */
  background-color: #b3b;
}

.stats {
  border-collapse: collapse;
  font-size: 12pt;
  table-layout: fixed;
  width: 100%;
  min-width: 450px;
}

.dark .stats td {
  border: 1px solid #bbb;
}

.stats td {
  border: 1px solid black;
  padding: 5px;
  word-wrap: break-word;
  text-align: center;
  position: relative;
}

#checkbox-stats div {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

#checkbox-stats .bar {
  background-color: rgba(28, 251, 0, 0.6);
}

.menu {
  position: relative;
  display: inline-block;
  margin: 0.4rem 0.4rem 0.4rem 0;
}

.menu-content {
  font-size: 12pt !important;
  text-align: left !important;
  font-weight: normal !important;
  display: none;
  position: absolute;
  background-color: white;
  right: 0;
  min-width: 300px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 100;
  padding: 8px;
}

.dark .menu-content {
  background-color: #111;
}

.menu:hover .menu-content {
  display: block;
}

.menu:hover .menubtn,
.menu:hover .iobtn,
.menu:hover .statsbtn {
  background-color: #eee;
}

.menu-label {
  display: inline-block;
  padding: 8px;
  border: 1px solid #ccc;
  border-top: 0;
  width: calc(100% - 18px);
}

.menu-label-top {
  border-top: 1px solid #ccc;
}

.menu-textbox {
  float: left;
  height: 24px;
  margin: 10px 5px;
  padding: 5px 5px;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 14px;
  box-sizing: border-box;
  border: 1px solid #888;
  border-radius: 4px;
  outline: none;
  background-color: #eee;
  transition: background-color 0.2s, border 0.2s;
  width: calc(100% - 10px);
}

.menu-textbox.invalid,
.dark .menu-textbox.invalid {
  color: red;
}

.dark .menu-textbox {
  background-color: #222;
  color: #eee;
}

.radio-container {
  margin: 4px;
}

.topmostdiv {
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: white;
  transition: background-color 0.3s;
  min-height: 100%;
}

#top {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
  align-items: center;
}

#topdivider {
  border-bottom: 2px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
}

.dark #topdivider {
  border-bottom: 2px solid #ccc;
}

#topdivider>div {
  position: relative;
}

#toptoggle {
  cursor: pointer;
  user-select: none;
  position: absolute;
  padding: 0.1rem 0.3rem;
  top: -0.4rem;
  left: -1rem;
  font-size: 1.4rem;
  line-height: 60%;
  border: 1px solid black;
  border-radius: 1rem;
  background-color: #fff;
  z-index: 100;
}

.flipped {
  transform: rotate(0.5turn);
}

.dark #toptoggle {
  border: 1px solid #fff;
  background-color: #222;
}

#fileinfodiv {
  flex: 20rem 1 0;
  overflow: auto;
}

#bomcontrols {
  display: flex;
  flex-direction: row-reverse;
}

#bomcontrols>* {
  flex-shrink: 0;
}

#dbg {
  display: block;
}

::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #aaa;
}

::-webkit-scrollbar-thumb {
  background: #666;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  margin: 3px 0;
  padding: 0;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
  border-radius: 3px;
}

.slider:hover {
  opacity: 1;
}

.slider:focus {
  outline: none;
}

.slider::-webkit-slider-runnable-track {
  -webkit-appearance: none;
  width: 100%;
  height: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  border: none;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
  margin-top: -4px;
}

.dark .slider::-webkit-slider-thumb {
  background: #3d3;
}

.slider::-moz-range-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
}

.slider::-moz-range-track {
  height: 8px;
  background: #d3d3d3;
  border-radius: 3px;
}

.dark .slider::-moz-range-thumb {
  background: #3d3;
}

.slider::-ms-track {
  width: 100%;
  height: 8px;
  border-width: 3px 0;
  background: transparent;
  border-color: transparent;
  color: transparent;
  transition: opacity .2s;
}

.slider::-ms-fill-lower {
  background: #d3d3d3;
  border: none;
  border-radius: 3px;
}

.slider::-ms-fill-upper {
  background: #d3d3d3;
  border: none;
  border-radius: 3px;
}

.slider::-ms-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
  margin: 0;
}

.shameless-plug {
  font-size: 0.8em;
  text-align: center;
  display: block;
}

a {
  color: #0278a4;
}

.dark a {
  color: #00b9fd;
}

#frontcanvas,
#backcanvas {
  touch-action: none;
}

.placeholder {
  border: 1px dashed #9f9fda !important;
  background-color: #edf2f7 !important;
}

.dragging {
  z-index: 999;
}

.dark .dragging>table>tbody>tr {
  background-color: #252c30;
}

.dark .placeholder {
  filter: invert(1);
}

.column-spacer {
  top: 0;
  left: 0;
  width: calc(100% - 4px);
  position: absolute;
  cursor: pointer;
  user-select: none;
  height: 100%;
}

.column-width-handle {
  top: 0;
  right: 0;
  width: 4px;
  position: absolute;
  cursor: col-resize;
  user-select: none;
  height: 100%;
}

.column-width-handle:hover {
  background-color: #4f99bd;
}

.help-link {
  border: 1px solid #0278a4;
  padding-inline: 0.3rem;
  border-radius: 3px;
  cursor: pointer;
}

.dark .help-link {
  border: 1px solid #00b9fd;
}

.bom-color {
  width: 20%;
}

.color-column input {
  width: 1.6rem;
  height: 1rem;
  border: 1px solid black;
  cursor: pointer;
  padding: 0;
}

/* removes default styling from input color element */
::-webkit-color-swatch {
  border: none;
}

::-webkit-color-swatch-wrapper {
  padding: 0;
}

::-moz-color-swatch,
::-moz-focus-inner {
  border: none;
}

::-moz-focus-inner {
  padding: 0;
}

  </style>
  <script type="text/javascript" >
///////////////////////////////////////////////
/*
  Split.js - v1.3.5
  MIT License
  https://github.com/nathancahill/Split.js
*/
!function(e,t){"object"==typeof exports&&"undefined"!=typeof module?module.exports=t():"function"==typeof define&&define.amd?define(t):e.Split=t()}(this,function(){"use strict";var e=window,t=e.document,n="addEventListener",i="removeEventListener",r="getBoundingClientRect",s=function(){return!1},o=e.attachEvent&&!e[n],a=["","-webkit-","-moz-","-o-"].filter(function(e){var n=t.createElement("div");return n.style.cssText="width:"+e+"calc(9px)",!!n.style.length}).shift()+"calc",l=function(e){return"string"==typeof e||e instanceof String?t.querySelector(e):e};return function(u,c){function z(e,t,n){var i=A(y,t,n);Object.keys(i).forEach(function(t){return e.style[t]=i[t]})}function h(e,t){var n=B(y,t);Object.keys(n).forEach(function(t){return e.style[t]=n[t]})}function f(e){var t=E[this.a],n=E[this.b],i=t.size+n.size;t.size=e/this.size*i,n.size=i-e/this.size*i,z(t.element,t.size,this.aGutterSize),z(n.element,n.size,this.bGutterSize)}function m(e){var t;this.dragging&&((t="touches"in e?e.touches[0][b]-this.start:e[b]-this.start)<=E[this.a].minSize+M+this.aGutterSize?t=E[this.a].minSize+this.aGutterSize:t>=this.size-(E[this.b].minSize+M+this.bGutterSize)&&(t=this.size-(E[this.b].minSize+this.bGutterSize)),f.call(this,t),c.onDrag&&c.onDrag())}function g(){var e=E[this.a].element,t=E[this.b].element;this.size=e[r]()[y]+t[r]()[y]+this.aGutterSize+this.bGutterSize,this.start=e[r]()[G]}function d(){var t=this,n=E[t.a].element,r=E[t.b].element;t.dragging&&c.onDragEnd&&c.onDragEnd(),t.dragging=!1,e[i]("mouseup",t.stop),e[i]("touchend",t.stop),e[i]("touchcancel",t.stop),t.parent[i]("mousemove",t.move),t.parent[i]("touchmove",t.move),delete t.stop,delete t.move,n[i]("selectstart",s),n[i]("dragstart",s),r[i]("selectstart",s),r[i]("dragstart",s),n.style.userSelect="",n.style.webkitUserSelect="",n.style.MozUserSelect="",n.style.pointerEvents="",r.style.userSelect="",r.style.webkitUserSelect="",r.style.MozUserSelect="",r.style.pointerEvents="",t.gutter.style.cursor="",t.parent.style.cursor=""}function S(t){var i=this,r=E[i.a].element,o=E[i.b].element;!i.dragging&&c.onDragStart&&c.onDragStart(),t.preventDefault(),i.dragging=!0,i.move=m.bind(i),i.stop=d.bind(i),e[n]("mouseup",i.stop),e[n]("touchend",i.stop),e[n]("touchcancel",i.stop),i.parent[n]("mousemove",i.move),i.parent[n]("touchmove",i.move),r[n]("selectstart",s),r[n]("dragstart",s),o[n]("selectstart",s),o[n]("dragstart",s),r.style.userSelect="none",r.style.webkitUserSelect="none",r.style.MozUserSelect="none",r.style.pointerEvents="none",o.style.userSelect="none",o.style.webkitUserSelect="none",o.style.MozUserSelect="none",o.style.pointerEvents="none",i.gutter.style.cursor=j,i.parent.style.cursor=j,g.call(i)}function v(e){e.forEach(function(t,n){if(n>0){var i=F[n-1],r=E[i.a],s=E[i.b];r.size=e[n-1],s.size=t,z(r.element,r.size,i.aGutterSize),z(s.element,s.size,i.bGutterSize)}})}function p(){F.forEach(function(e){e.parent.removeChild(e.gutter),E[e.a].element.style[y]="",E[e.b].element.style[y]=""})}void 0===c&&(c={});var y,b,G,E,w=l(u[0]).parentNode,D=e.getComputedStyle(w).flexDirection,U=c.sizes||u.map(function(){return 100/u.length}),k=void 0!==c.minSize?c.minSize:100,x=Array.isArray(k)?k:u.map(function(){return k}),L=void 0!==c.gutterSize?c.gutterSize:10,M=void 0!==c.snapOffset?c.snapOffset:30,O=c.direction||"horizontal",j=c.cursor||("horizontal"===O?"ew-resize":"ns-resize"),C=c.gutter||function(e,n){var i=t.createElement("div");return i.className="gutter gutter-"+n,i},A=c.elementStyle||function(e,t,n){var i={};return"string"==typeof t||t instanceof String?i[e]=t:i[e]=o?t+"%":a+"("+t+"% - "+n+"px)",i},B=c.gutterStyle||function(e,t){return n={},n[e]=t+"px",n;var n};"horizontal"===O?(y="width","clientWidth",b="clientX",G="left","paddingLeft"):"vertical"===O&&(y="height","clientHeight",b="clientY",G="top","paddingTop");var F=[];return E=u.map(function(e,t){var i,s={element:l(e),size:U[t],minSize:x[t]};if(t>0&&(i={a:t-1,b:t,dragging:!1,isFirst:1===t,isLast:t===u.length-1,direction:O,parent:w},i.aGutterSize=L,i.bGutterSize=L,i.isFirst&&(i.aGutterSize=L/2),i.isLast&&(i.bGutterSize=L/2),"row-reverse"===D||"column-reverse"===D)){var a=i.a;i.a=i.b,i.b=a}if(!o&&t>0){var c=C(t,O);h(c,L),c[n]("mousedown",S.bind(i)),c[n]("touchstart",S.bind(i)),w.insertBefore(c,s.element),i.gutter=c}0===t||t===u.length-1?z(s.element,s.size,L/2):z(s.element,s.size,L);var f=s.element[r]()[y];return f<s.minSize&&(s.minSize=f),t>0&&F.push(i),s}),o?{setSizes:v,destroy:p}:{setSizes:v,getSizes:function(){return E.map(function(e){return e.size})},collapse:function(e){if(e===F.length){var t=F[e-1];g.call(t),o||f.call(t,t.size-t.bGutterSize)}else{var n=F[e];g.call(n),o||f.call(n,n.aGutterSize)}},destroy:p}}});

///////////////////////////////////////////////

///////////////////////////////////////////////
// Copyright (c) 2013 Pieroxy <pieroxy@pieroxy.net>
// This work is free. You can redistribute it and/or modify it
// under the terms of the WTFPL, Version 2
// For more information see LICENSE.txt or http://www.wtfpl.net/
//
// For more information, the home page:
// http://pieroxy.net/blog/pages/lz-string/testing.html
//
// LZ-based compression algorithm, version 1.4.4
var LZString=function(){var o=String.fromCharCode,i={};var n={decompressFromBase64:function(o){return null==o?"":""==o?null:n._decompress(o.length,32,function(n){return function(o,n){if(!i[o]){i[o]={};for(var t=0;t<o.length;t++)i[o][o.charAt(t)]=t}return i[o][n]}("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",o.charAt(n))})},_decompress:function(i,n,t){var r,e,a,s,p,u,l,f=[],c=4,d=4,h=3,v="",g=[],m={val:t(0),position:n,index:1};for(r=0;r<3;r+=1)f[r]=r;for(a=0,p=Math.pow(2,2),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;switch(a){case 0:for(a=0,p=Math.pow(2,8),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;l=o(a);break;case 1:for(a=0,p=Math.pow(2,16),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;l=o(a);break;case 2:return""}for(f[3]=l,e=l,g.push(l);;){if(m.index>i)return"";for(a=0,p=Math.pow(2,h),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;switch(l=a){case 0:for(a=0,p=Math.pow(2,8),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;f[d++]=o(a),l=d-1,c--;break;case 1:for(a=0,p=Math.pow(2,16),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;f[d++]=o(a),l=d-1,c--;break;case 2:return g.join("")}if(0==c&&(c=Math.pow(2,h),h++),f[l])v=f[l];else{if(l!==d)return null;v=e+e.charAt(0)}g.push(v),f[d++]=e+v.charAt(0),e=v,0==--c&&(c=Math.pow(2,h),h++)}}};return n}();"function"==typeof define&&define.amd?define(function(){return LZString}):"undefined"!=typeof module&&null!=module?module.exports=LZString:"undefined"!=typeof angular&&null!=angular&&angular.module("LZString",[]).factory("LZString",function(){return LZString});
///////////////////////////////////////////////

///////////////////////////////////////////////
/*!
 * PEP v0.4.3 | https://github.com/jquery/PEP
 * Copyright jQuery Foundation and other contributors | http://jquery.org/license
 */
!function(a,b){"object"==typeof exports&&"undefined"!=typeof module?module.exports=b():"function"==typeof define&&define.amd?define(b):a.PointerEventsPolyfill=b()}(this,function(){"use strict";function a(a,b){b=b||Object.create(null);var c=document.createEvent("Event");c.initEvent(a,b.bubbles||!1,b.cancelable||!1);
for(var d,e=2;e<m.length;e++)d=m[e],c[d]=b[d]||n[e];c.buttons=b.buttons||0;
var f=0;return f=b.pressure&&c.buttons?b.pressure:c.buttons?.5:0,c.x=c.clientX,c.y=c.clientY,c.pointerId=b.pointerId||0,c.width=b.width||0,c.height=b.height||0,c.pressure=f,c.tiltX=b.tiltX||0,c.tiltY=b.tiltY||0,c.twist=b.twist||0,c.tangentialPressure=b.tangentialPressure||0,c.pointerType=b.pointerType||"",c.hwTimestamp=b.hwTimestamp||0,c.isPrimary=b.isPrimary||!1,c}function b(){this.array=[],this.size=0}function c(a,b,c,d){this.addCallback=a.bind(d),this.removeCallback=b.bind(d),this.changedCallback=c.bind(d),A&&(this.observer=new A(this.mutationWatcher.bind(this)))}function d(a){return"body /shadow-deep/ "+e(a)}function e(a){return'[touch-action="'+a+'"]'}function f(a){return"{ -ms-touch-action: "+a+"; touch-action: "+a+"; }"}function g(){if(F){D.forEach(function(a){String(a)===a?(E+=e(a)+f(a)+"\n",G&&(E+=d(a)+f(a)+"\n")):(E+=a.selectors.map(e)+f(a.rule)+"\n",G&&(E+=a.selectors.map(d)+f(a.rule)+"\n"))});var a=document.createElement("style");a.textContent=E,document.head.appendChild(a)}}function h(){if(!window.PointerEvent){if(window.PointerEvent=a,window.navigator.msPointerEnabled){var b=window.navigator.msMaxTouchPoints;Object.defineProperty(window.navigator,"maxTouchPoints",{value:b,enumerable:!0}),u.registerSource("ms",_)}else Object.defineProperty(window.navigator,"maxTouchPoints",{value:0,enumerable:!0}),u.registerSource("mouse",N),void 0!==window.ontouchstart&&u.registerSource("touch",V);u.register(document)}}function i(a){if(!u.pointermap.has(a)){var b=new Error("InvalidPointerId");throw b.name="InvalidPointerId",b}}function j(a){for(var b=a.parentNode;b&&b!==a.ownerDocument;)b=b.parentNode;if(!b){var c=new Error("InvalidStateError");throw c.name="InvalidStateError",c}}function k(a){var b=u.pointermap.get(a);return 0!==b.buttons}function l(){window.Element&&!Element.prototype.setPointerCapture&&Object.defineProperties(Element.prototype,{setPointerCapture:{value:W},releasePointerCapture:{value:X},hasPointerCapture:{value:Y}})}
var m=["bubbles","cancelable","view","detail","screenX","screenY","clientX","clientY","ctrlKey","altKey","shiftKey","metaKey","button","relatedTarget","pageX","pageY"],n=[!1,!1,null,null,0,0,0,0,!1,!1,!1,!1,0,null,0,0],o=window.Map&&window.Map.prototype.forEach,p=o?Map:b;b.prototype={set:function(a,b){return void 0===b?this["delete"](a):(this.has(a)||this.size++,void(this.array[a]=b))},has:function(a){return void 0!==this.array[a]},"delete":function(a){this.has(a)&&(delete this.array[a],this.size--)},get:function(a){return this.array[a]},clear:function(){this.array.length=0,this.size=0},forEach:function(a,b){return this.array.forEach(function(c,d){a.call(b,c,d,this)},this)}};var q=["bubbles","cancelable","view","detail","screenX","screenY","clientX","clientY","ctrlKey","altKey","shiftKey","metaKey","button","relatedTarget","buttons","pointerId","width","height","pressure","tiltX","tiltY","pointerType","hwTimestamp","isPrimary","type","target","currentTarget","which","pageX","pageY","timeStamp"],r=[!1,!1,null,null,0,0,0,0,!1,!1,!1,!1,0,null,0,0,0,0,0,0,0,"",0,!1,"",null,null,0,0,0,0],s={pointerover:1,pointerout:1,pointerenter:1,pointerleave:1},t="undefined"!=typeof SVGElementInstance,u={pointermap:new p,eventMap:Object.create(null),captureInfo:Object.create(null),eventSources:Object.create(null),eventSourceList:[],registerSource:function(a,b){var c=b,d=c.events;d&&(d.forEach(function(a){c[a]&&(this.eventMap[a]=c[a].bind(c))},this),this.eventSources[a]=c,this.eventSourceList.push(c))},register:function(a){for(var b,c=this.eventSourceList.length,d=0;d<c&&(b=this.eventSourceList[d]);d++)
b.register.call(b,a)},unregister:function(a){for(var b,c=this.eventSourceList.length,d=0;d<c&&(b=this.eventSourceList[d]);d++)
b.unregister.call(b,a)},contains:function(a,b){try{return a.contains(b)}catch(c){return!1}},down:function(a){a.bubbles=!0,this.fireEvent("pointerdown",a)},move:function(a){a.bubbles=!0,this.fireEvent("pointermove",a)},up:function(a){a.bubbles=!0,this.fireEvent("pointerup",a)},enter:function(a){a.bubbles=!1,this.fireEvent("pointerenter",a)},leave:function(a){a.bubbles=!1,this.fireEvent("pointerleave",a)},over:function(a){a.bubbles=!0,this.fireEvent("pointerover",a)},out:function(a){a.bubbles=!0,this.fireEvent("pointerout",a)},cancel:function(a){a.bubbles=!0,this.fireEvent("pointercancel",a)},leaveOut:function(a){this.out(a),this.propagate(a,this.leave,!1)},enterOver:function(a){this.over(a),this.propagate(a,this.enter,!0)},eventHandler:function(a){if(!a._handledByPE){var b=a.type,c=this.eventMap&&this.eventMap[b];c&&c(a),a._handledByPE=!0}},listen:function(a,b){b.forEach(function(b){this.addEvent(a,b)},this)},unlisten:function(a,b){b.forEach(function(b){this.removeEvent(a,b)},this)},addEvent:function(a,b){a.addEventListener(b,this.boundHandler)},removeEvent:function(a,b){a.removeEventListener(b,this.boundHandler)},makeEvent:function(b,c){this.captureInfo[c.pointerId]&&(c.relatedTarget=null);var d=new a(b,c);return c.preventDefault&&(d.preventDefault=c.preventDefault),d._target=d._target||c.target,d},fireEvent:function(a,b){var c=this.makeEvent(a,b);return this.dispatchEvent(c)},cloneEvent:function(a){for(var b,c=Object.create(null),d=0;d<q.length;d++)b=q[d],c[b]=a[b]||r[d],!t||"target"!==b&&"relatedTarget"!==b||c[b]instanceof SVGElementInstance&&(c[b]=c[b].correspondingUseElement);return a.preventDefault&&(c.preventDefault=function(){a.preventDefault()}),c},getTarget:function(a){var b=this.captureInfo[a.pointerId];return b?a._target!==b&&a.type in s?void 0:b:a._target},propagate:function(a,b,c){for(var d=a.target,e=[];d!==document&&!d.contains(a.relatedTarget);) if(e.push(d),d=d.parentNode,!d)return;c&&e.reverse(),e.forEach(function(c){a.target=c,b.call(this,a)},this)},setCapture:function(b,c,d){this.captureInfo[b]&&this.releaseCapture(b,d),this.captureInfo[b]=c,this.implicitRelease=this.releaseCapture.bind(this,b,d),document.addEventListener("pointerup",this.implicitRelease),document.addEventListener("pointercancel",this.implicitRelease);var e=new a("gotpointercapture");e.pointerId=b,e._target=c,d||this.asyncDispatchEvent(e)},releaseCapture:function(b,c){var d=this.captureInfo[b];if(d){this.captureInfo[b]=void 0,document.removeEventListener("pointerup",this.implicitRelease),document.removeEventListener("pointercancel",this.implicitRelease);var e=new a("lostpointercapture");e.pointerId=b,e._target=d,c||this.asyncDispatchEvent(e)}},dispatchEvent:/*scope.external.dispatchEvent || */function(a){var b=this.getTarget(a);if(b)return b.dispatchEvent(a)},asyncDispatchEvent:function(a){requestAnimationFrame(this.dispatchEvent.bind(this,a))}};u.boundHandler=u.eventHandler.bind(u);var v={shadow:function(a){if(a)return a.shadowRoot||a.webkitShadowRoot},canTarget:function(a){return a&&Boolean(a.elementFromPoint)},targetingShadow:function(a){var b=this.shadow(a);if(this.canTarget(b))return b},olderShadow:function(a){var b=a.olderShadowRoot;if(!b){var c=a.querySelector("shadow");c&&(b=c.olderShadowRoot)}return b},allShadows:function(a){for(var b=[],c=this.shadow(a);c;)b.push(c),c=this.olderShadow(c);return b},searchRoot:function(a,b,c){if(a){var d,e,f=a.elementFromPoint(b,c);for(e=this.targetingShadow(f);e;){if(d=e.elementFromPoint(b,c)){var g=this.targetingShadow(d);return this.searchRoot(g,b,c)||d} e=this.olderShadow(e)} return f}},owner:function(a){
for(var b=a;b.parentNode;)b=b.parentNode;
return b.nodeType!==Node.DOCUMENT_NODE&&b.nodeType!==Node.DOCUMENT_FRAGMENT_NODE&&(b=document),b},findTarget:function(a){var b=a.clientX,c=a.clientY,d=this.owner(a.target);
return d.elementFromPoint(b,c)||(d=document),this.searchRoot(d,b,c)}},w=Array.prototype.forEach.call.bind(Array.prototype.forEach),x=Array.prototype.map.call.bind(Array.prototype.map),y=Array.prototype.slice.call.bind(Array.prototype.slice),z=Array.prototype.filter.call.bind(Array.prototype.filter),A=window.MutationObserver||window.WebKitMutationObserver,B="[touch-action]",C={subtree:!0,childList:!0,attributes:!0,attributeOldValue:!0,attributeFilter:["touch-action"]};c.prototype={watchSubtree:function(a){
//
this.observer&&v.canTarget(a)&&this.observer.observe(a,C)},enableOnSubtree:function(a){this.watchSubtree(a),a===document&&"complete"!==document.readyState?this.installOnLoad():this.installNewSubtree(a)},installNewSubtree:function(a){w(this.findElements(a),this.addElement,this)},findElements:function(a){return a.querySelectorAll?a.querySelectorAll(B):[]},removeElement:function(a){this.removeCallback(a)},addElement:function(a){this.addCallback(a)},elementChanged:function(a,b){this.changedCallback(a,b)},concatLists:function(a,b){return a.concat(y(b))},
installOnLoad:function(){document.addEventListener("readystatechange",function(){"complete"===document.readyState&&this.installNewSubtree(document)}.bind(this))},isElement:function(a){return a.nodeType===Node.ELEMENT_NODE},flattenMutationTree:function(a){
var b=x(a,this.findElements,this);
return b.push(z(a,this.isElement)),b.reduce(this.concatLists,[])},mutationWatcher:function(a){a.forEach(this.mutationHandler,this)},mutationHandler:function(a){if("childList"===a.type){var b=this.flattenMutationTree(a.addedNodes);b.forEach(this.addElement,this);var c=this.flattenMutationTree(a.removedNodes);c.forEach(this.removeElement,this)}else"attributes"===a.type&&this.elementChanged(a.target,a.oldValue)}};var D=["none","auto","pan-x","pan-y",{rule:"pan-x pan-y",selectors:["pan-x pan-y","pan-y pan-x"]}],E="",F=window.PointerEvent||window.MSPointerEvent,G=!window.ShadowDOMPolyfill&&document.head.createShadowRoot,H=u.pointermap,I=25,J=[1,4,2,8,16],K=!1;try{K=1===new MouseEvent("test",{buttons:1}).buttons}catch(L){}
var M,N={POINTER_ID:1,POINTER_TYPE:"mouse",events:["mousedown","mousemove","mouseup","mouseover","mouseout"],register:function(a){u.listen(a,this.events)},unregister:function(a){u.unlisten(a,this.events)},lastTouches:[],
isEventSimulatedFromTouch:function(a){for(var b,c=this.lastTouches,d=a.clientX,e=a.clientY,f=0,g=c.length;f<g&&(b=c[f]);f++){
var h=Math.abs(d-b.x),i=Math.abs(e-b.y);if(h<=I&&i<=I)return!0}},prepareEvent:function(a){var b=u.cloneEvent(a),c=b.preventDefault;return b.preventDefault=function(){a.preventDefault(),c()},b.pointerId=this.POINTER_ID,b.isPrimary=!0,b.pointerType=this.POINTER_TYPE,b},prepareButtonsForMove:function(a,b){var c=H.get(this.POINTER_ID);
0!==b.which&&c?a.buttons=c.buttons:a.buttons=0,b.buttons=a.buttons},mousedown:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=H.get(this.POINTER_ID),c=this.prepareEvent(a);K||(c.buttons=J[c.button],b&&(c.buttons|=b.buttons),a.buttons=c.buttons),H.set(this.POINTER_ID,a),b&&0!==b.buttons?u.move(c):u.down(c)}},mousemove:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,H.set(this.POINTER_ID,a),u.move(b)}},mouseup:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=H.get(this.POINTER_ID),c=this.prepareEvent(a);if(!K){var d=J[c.button];
c.buttons=b?b.buttons&~d:0,a.buttons=c.buttons}H.set(this.POINTER_ID,a),
c.buttons&=~J[c.button],0===c.buttons?u.up(c):u.move(c)}},mouseover:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,H.set(this.POINTER_ID,a),u.enterOver(b)}},mouseout:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,u.leaveOut(b)}},cancel:function(a){var b=this.prepareEvent(a);u.cancel(b),this.deactivateMouse()},deactivateMouse:function(){H["delete"](this.POINTER_ID)}},O=u.captureInfo,P=v.findTarget.bind(v),Q=v.allShadows.bind(v),R=u.pointermap,S=2500,T=200,U="touch-action",V={events:["touchstart","touchmove","touchend","touchcancel"],register:function(a){M.enableOnSubtree(a)},unregister:function(){},elementAdded:function(a){var b=a.getAttribute(U),c=this.touchActionToScrollType(b);c&&(a._scrollType=c,u.listen(a,this.events),
Q(a).forEach(function(a){a._scrollType=c,u.listen(a,this.events)},this))},elementRemoved:function(a){a._scrollType=void 0,u.unlisten(a,this.events),
Q(a).forEach(function(a){a._scrollType=void 0,u.unlisten(a,this.events)},this)},elementChanged:function(a,b){var c=a.getAttribute(U),d=this.touchActionToScrollType(c),e=this.touchActionToScrollType(b);
d&&e?(a._scrollType=d,Q(a).forEach(function(a){a._scrollType=d},this)):e?this.elementRemoved(a):d&&this.elementAdded(a)},scrollTypes:{EMITTER:"none",XSCROLLER:"pan-x",YSCROLLER:"pan-y",SCROLLER:/^(?:pan-x pan-y)|(?:pan-y pan-x)|auto$/},touchActionToScrollType:function(a){var b=a,c=this.scrollTypes;return"none"===b?"none":b===c.XSCROLLER?"X":b===c.YSCROLLER?"Y":c.SCROLLER.exec(b)?"XY":void 0},POINTER_TYPE:"touch",firstTouch:null,isPrimaryTouch:function(a){return this.firstTouch===a.identifier},setPrimaryTouch:function(a){
(0===R.size||1===R.size&&R.has(1))&&(this.firstTouch=a.identifier,this.firstXY={X:a.clientX,Y:a.clientY},this.scrolling=!1,this.cancelResetClickCount())},removePrimaryPointer:function(a){a.isPrimary&&(this.firstTouch=null,this.firstXY=null,this.resetClickCount())},clickCount:0,resetId:null,resetClickCount:function(){var a=function(){this.clickCount=0,this.resetId=null}.bind(this);this.resetId=setTimeout(a,T)},cancelResetClickCount:function(){this.resetId&&clearTimeout(this.resetId)},typeToButtons:function(a){var b=0;return"touchstart"!==a&&"touchmove"!==a||(b=1),b},touchToPointer:function(a){var b=this.currentTouchEvent,c=u.cloneEvent(a),d=c.pointerId=a.identifier+2;c.target=O[d]||P(c),c.bubbles=!0,c.cancelable=!0,c.detail=this.clickCount,c.button=0,c.buttons=this.typeToButtons(b.type),c.width=2*(a.radiusX||a.webkitRadiusX||0),c.height=2*(a.radiusY||a.webkitRadiusY||0),c.pressure=a.force||a.webkitForce||.5,c.isPrimary=this.isPrimaryTouch(a),c.pointerType=this.POINTER_TYPE,
c.altKey=b.altKey,c.ctrlKey=b.ctrlKey,c.metaKey=b.metaKey,c.shiftKey=b.shiftKey;
var e=this;return c.preventDefault=function(){e.scrolling=!1,e.firstXY=null,b.preventDefault()},c},processTouches:function(a,b){var c=a.changedTouches;this.currentTouchEvent=a;for(var d,e=0;e<c.length;e++)d=c[e],b.call(this,this.touchToPointer(d))},
shouldScroll:function(a){if(this.firstXY){var b,c=a.currentTarget._scrollType;if("none"===c)
b=!1;else if("XY"===c)
b=!0;else{var d=a.changedTouches[0],e=c,f="Y"===c?"X":"Y",g=Math.abs(d["client"+e]-this.firstXY[e]),h=Math.abs(d["client"+f]-this.firstXY[f]);
b=g>=h}return this.firstXY=null,b}},findTouch:function(a,b){for(var c,d=0,e=a.length;d<e&&(c=a[d]);d++)if(c.identifier===b)return!0},
vacuumTouches:function(a){var b=a.touches;
if(R.size>=b.length){var c=[];R.forEach(function(a,d){
if(1!==d&&!this.findTouch(b,d-2)){var e=a.out;c.push(e)}},this),c.forEach(this.cancelOut,this)}},touchstart:function(a){this.vacuumTouches(a),this.setPrimaryTouch(a.changedTouches[0]),this.dedupSynthMouse(a),this.scrolling||(this.clickCount++,this.processTouches(a,this.overDown))},overDown:function(a){R.set(a.pointerId,{target:a.target,out:a,outTarget:a.target}),u.enterOver(a),u.down(a)},touchmove:function(a){this.scrolling||(this.shouldScroll(a)?(this.scrolling=!0,this.touchcancel(a)):(a.preventDefault(),this.processTouches(a,this.moveOverOut)))},moveOverOut:function(a){var b=a,c=R.get(b.pointerId);
if(c){var d=c.out,e=c.outTarget;u.move(b),d&&e!==b.target&&(d.relatedTarget=b.target,b.relatedTarget=e,
d.target=e,b.target?(u.leaveOut(d),u.enterOver(b)):(
b.target=e,b.relatedTarget=null,this.cancelOut(b))),c.out=b,c.outTarget=b.target}},touchend:function(a){this.dedupSynthMouse(a),this.processTouches(a,this.upOut)},upOut:function(a){this.scrolling||(u.up(a),u.leaveOut(a)),this.cleanUpPointer(a)},touchcancel:function(a){this.processTouches(a,this.cancelOut)},cancelOut:function(a){u.cancel(a),u.leaveOut(a),this.cleanUpPointer(a)},cleanUpPointer:function(a){R["delete"](a.pointerId),this.removePrimaryPointer(a)},
dedupSynthMouse:function(a){var b=N.lastTouches,c=a.changedTouches[0];
if(this.isPrimaryTouch(c)){
var d={x:c.clientX,y:c.clientY};b.push(d);var e=function(a,b){var c=a.indexOf(b);c>-1&&a.splice(c,1)}.bind(null,b,d);setTimeout(e,S)}}};M=new c(V.elementAdded,V.elementRemoved,V.elementChanged,V);var W,X,Y,Z=u.pointermap,$=window.MSPointerEvent&&"number"==typeof window.MSPointerEvent.MSPOINTER_TYPE_MOUSE,_={events:["MSPointerDown","MSPointerMove","MSPointerUp","MSPointerOut","MSPointerOver","MSPointerCancel","MSGotPointerCapture","MSLostPointerCapture"],register:function(a){u.listen(a,this.events)},unregister:function(a){u.unlisten(a,this.events)},POINTER_TYPES:["","unavailable","touch","pen","mouse"],prepareEvent:function(a){var b=a;return $&&(b=u.cloneEvent(a),b.pointerType=this.POINTER_TYPES[a.pointerType]),b},cleanup:function(a){Z["delete"](a)},MSPointerDown:function(a){Z.set(a.pointerId,a);var b=this.prepareEvent(a);u.down(b)},MSPointerMove:function(a){var b=this.prepareEvent(a);u.move(b)},MSPointerUp:function(a){var b=this.prepareEvent(a);u.up(b),this.cleanup(a.pointerId)},MSPointerOut:function(a){var b=this.prepareEvent(a);u.leaveOut(b)},MSPointerOver:function(a){var b=this.prepareEvent(a);u.enterOver(b)},MSPointerCancel:function(a){var b=this.prepareEvent(a);u.cancel(b),this.cleanup(a.pointerId)},MSLostPointerCapture:function(a){var b=u.makeEvent("lostpointercapture",a);u.dispatchEvent(b)},MSGotPointerCapture:function(a){var b=u.makeEvent("gotpointercapture",a);u.dispatchEvent(b)}},aa=window.navigator;aa.msPointerEnabled?(W=function(a){i(a),j(this),k(a)&&(u.setCapture(a,this,!0),this.msSetPointerCapture(a))},X=function(a){i(a),u.releaseCapture(a,!0),this.msReleasePointerCapture(a)}):(W=function(a){i(a),j(this),k(a)&&u.setCapture(a,this)},X=function(a){i(a),u.releaseCapture(a)}),Y=function(a){return!!u.captureInfo[a]},g(),h(),l();var ba={dispatcher:u,Installer:c,PointerEvent:a,PointerMap:p,targetFinding:v};return ba});

///////////////////////////////////////////////

///////////////////////////////////////////////
var config = {"dark_mode": false, "show_pads": true, "show_fabrication": false, "show_silkscreen": true, "highlight_pin1": "none", "redraw_on_drag": true, "board_rotation": 0, "checkboxes": "Sourced,Placed", "bom_view": "left-right", "layer_view": "FB", "offset_back_rotation": false, "kicad_text_formatting": true, "fields": ["Value", "Footprint"]}
///////////////////////////////////////////////

///////////////////////////////////////////////
var pcbdata = JSON.parse(LZString.decompressFromBase64("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"))
///////////////////////////////////////////////

///////////////////////////////////////////////
/* Utility functions */

var storagePrefix = 'KiCad_HTML_BOM__' + pcbdata.metadata.title + '__' +
  pcbdata.metadata.revision + '__#';
var storage;

function initStorage(key) {
  try {
    window.localStorage.getItem("blank");
    storage = window.localStorage;
  } catch (e) {
    // localStorage not available
  }
  if (!storage) {
    try {
      window.sessionStorage.getItem("blank");
      storage = window.sessionStorage;
    } catch (e) {
      // sessionStorage also not available
    }
  }
}

function readStorage(key) {
  if (storage) {
    return storage.getItem(storagePrefix + key);
  } else {
    return null;
  }
}

function writeStorage(key, value) {
  if (storage) {
    storage.setItem(storagePrefix + key, value);
  }
}

function fancyDblClickHandler(el, onsingle, ondouble) {
  return function () {
    if (el.getAttribute("data-dblclick") == null) {
      el.setAttribute("data-dblclick", 1);
      setTimeout(function () {
        if (el.getAttribute("data-dblclick") == 1) {
          onsingle();
        }
        el.removeAttribute("data-dblclick");
      }, 200);
    } else {
      el.removeAttribute("data-dblclick");
      ondouble();
    }
  }
}

function smoothScrollToRow(rowid) {
  document.getElementById(rowid).scrollIntoView({
    behavior: "smooth",
    block: "center",
    inline: "nearest"
  });
}

function focusInputField(input) {
  input.scrollIntoView(false);
  input.focus();
  input.select();
}

function saveBomTable(output) {
  var text = '';
  for (var node of bomhead.childNodes[0].childNodes) {
    if (node.firstChild) {
      var name = node.firstChild.nodeValue ?? "";
      text += (output == 'csv' ? `"${name}"` : name);
    }
    if (node != bomhead.childNodes[0].lastChild) {
      text += (output == 'csv' ? ',' : '\t');
    }
  }
  text += '\n';
  for (var row of bombody.childNodes) {
    for (var cell of row.childNodes) {
      let val = '';
      for (var node of cell.childNodes) {
        if (node.nodeName == "INPUT") {
          if (node.checked) {
            val += '✓';
          }
        } else if ((node.nodeName == "MARK") || (node.nodeName == "A")) {
          val += node.firstChild.nodeValue;
        } else {
          val += node.nodeValue;
        }
      }
      if (output == 'csv') {
        val = val.replace(/\"/g, '\"\"'); // pair of double-quote characters
        if (isNumeric(val)) {
          val = +val;                     // use number
        } else {
          val = `"${val}"`;               // enclosed within double-quote
        }
      }
      text += val;
      if (cell != row.lastChild) {
        text += (output == 'csv' ? ',' : '\t');
      }
    }
    text += '\n';
  }

  if (output != 'clipboard') {
    // To file: csv or txt
    var blob = new Blob([text], {
      type: `text/${output}`
    });
    saveFile(`${pcbdata.metadata.title}.${output}`, blob);
  } else {
    // To clipboard
    var textArea = document.createElement("textarea");
    textArea.classList.add('clipboard-temp');
    textArea.value = text;

    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
      if (document.execCommand('copy')) {
        console.log('Bom copied to clipboard.');
      }
    } catch (err) {
      console.log('Can not copy to clipboard.');
    }

    document.body.removeChild(textArea);
  }
}

function isNumeric(str) {
  /* https://stackoverflow.com/a/175787 */
  return (typeof str != "string" ? false : !isNaN(str) && !isNaN(parseFloat(str)));
}

function removeGutterNode(node) {
  for (var i = 0; i < node.childNodes.length; i++) {
    if (node.childNodes[i].classList &&
      node.childNodes[i].classList.contains("gutter")) {
      node.removeChild(node.childNodes[i]);
      break;
    }
  }
}

function cleanGutters() {
  removeGutterNode(document.getElementById("bot"));
  removeGutterNode(document.getElementById("canvasdiv"));
}

var units = {
  prefixes: {
    giga: ["G", "g", "giga", "Giga", "GIGA"],
    mega: ["M", "mega", "Mega", "MEGA"],
    kilo: ["K", "k", "kilo", "Kilo", "KILO"],
    milli: ["m", "milli", "Milli", "MILLI"],
    micro: ["U", "u", "micro", "Micro", "MICRO", "μ", "µ"], // different utf8 μ
    nano: ["N", "n", "nano", "Nano", "NANO"],
    pico: ["P", "p", "pico", "Pico", "PICO"],
  },
  unitsShort: ["R", "r", "Ω", "F", "f", "H", "h"],
  unitsLong: [
    "OHM", "Ohm", "ohm", "ohms",
    "FARAD", "Farad", "farad",
    "HENRY", "Henry", "henry"
  ],
  getMultiplier: function (s) {
    if (this.prefixes.giga.includes(s)) return 1e9;
    if (this.prefixes.mega.includes(s)) return 1e6;
    if (this.prefixes.kilo.includes(s)) return 1e3;
    if (this.prefixes.milli.includes(s)) return 1e-3;
    if (this.prefixes.micro.includes(s)) return 1e-6;
    if (this.prefixes.nano.includes(s)) return 1e-9;
    if (this.prefixes.pico.includes(s)) return 1e-12;
    return 1;
  },
  valueRegex: null,
  valueAltRegex: null,
}

function initUtils() {
  var allPrefixes = units.prefixes.giga
    .concat(units.prefixes.mega)
    .concat(units.prefixes.kilo)
    .concat(units.prefixes.milli)
    .concat(units.prefixes.micro)
    .concat(units.prefixes.nano)
    .concat(units.prefixes.pico);
  var allUnits = units.unitsShort.concat(units.unitsLong);
  units.valueRegex = new RegExp("^([0-9\.]+)" +
    "\\s*(" + allPrefixes.join("|") + ")?" +
    "(" + allUnits.join("|") + ")?" +
    "(\\b.*)?$", "");
  units.valueAltRegex = new RegExp("^([0-9]*)" +
    "(" + units.unitsShort.join("|") + ")?" +
    "([GgMmKkUuNnPp])?" +
    "([0-9]*)" +
    "(\\b.*)?$", "");
  if (config.fields.includes("Value")) {
    var index = config.fields.indexOf("Value");
    pcbdata.bom["parsedValues"] = {};
    var allList = getBomListByLayer('FB').flat();
    for (var id in pcbdata.bom.fields) {
      var ref_key = allList.find(item => item[1] == Number(id)) || [];
      pcbdata.bom.parsedValues[id] = parseValue(pcbdata.bom.fields[id][index], ref_key[0] || '');
    }
  }
}

function parseValue(val, ref) {
  var inferUnit = (unit, ref) => {
    if (unit) {
      unit = unit.toLowerCase();
      if (unit == 'Ω' || unit == "ohm" || unit == "ohms") {
        unit = 'r';
      }
      return unit[0];
    }

    var resarr = /^([a-z]+)\d+$/i.exec(ref);
    switch (Array.isArray(resarr) && resarr[1].toLowerCase()) {
      case "c": return 'f';
      case "l": return 'h';
      case "r":
      case "rv": return 'r';
    }
    return null;
  };
  val = val.replace(/,/g, "");
  var match = units.valueRegex.exec(val);
  if (Array.isArray(match)) {
    var unit = inferUnit(match[3], ref);
    var val_i = parseFloat(match[1]);
    if (!unit) return null;
    if (match[2]) {
      val_i = val_i * units.getMultiplier(match[2]);
    }
    return {
      val: val_i,
      unit: unit,
      extra: match[4],
    }
  }

  match = units.valueAltRegex.exec(val);
  if (Array.isArray(match) && (match[1] || match[4])) {
    var unit = inferUnit(match[2], ref);
    var val_i = parseFloat(match[1] + "." + match[4]);
    if (!unit) return null;
    if (match[3]) {
      val_i = val_i * units.getMultiplier(match[3]);
    }
    return {
      val: val_i,
      unit: unit,
      extra: match[5],
    }
  }
  return null;
}

function valueCompare(a, b, stra, strb) {
  if (a === null && b === null) {
    // Failed to parse both values, compare them as strings.
    if (stra != strb) return stra > strb ? 1 : -1;
    else return 0;
  } else if (a === null) {
    return 1;
  } else if (b === null) {
    return -1;
  } else {
    if (a.unit != b.unit) return a.unit > b.unit ? 1 : -1;
    else if (a.val != b.val) return a.val > b.val ? 1 : -1;
    else if (a.extra != b.extra) return a.extra > b.extra ? 1 : -1;
    else return 0;
  }
}

function validateSaveImgDimension(element) {
  var valid = false;
  var intValue = 0;
  if (/^[1-9]\d*$/.test(element.value)) {
    intValue = parseInt(element.value);
    if (intValue <= 16000) {
      valid = true;
    }
  }
  if (valid) {
    element.classList.remove("invalid");
  } else {
    element.classList.add("invalid");
  }
  return intValue;
}

function saveImage(layer) {
  var width = validateSaveImgDimension(document.getElementById("render-save-width"));
  var height = validateSaveImgDimension(document.getElementById("render-save-height"));
  var bgcolor = null;
  if (!document.getElementById("render-save-transparent").checked) {
    var style = getComputedStyle(topmostdiv);
    bgcolor = style.getPropertyValue("background-color");
  }
  if (!width || !height) return;

  // Prepare image
  var canvas = document.createElement("canvas");
  var layerdict = {
    transform: {
      x: 0,
      y: 0,
      s: 1,
      panx: 0,
      pany: 0,
      zoom: 1,
    },
    bg: canvas,
    fab: canvas,
    silk: canvas,
    highlight: canvas,
    layer: layer,
  }
  // Do the rendering
  recalcLayerScale(layerdict, width, height);
  prepareLayer(layerdict);
  clearCanvas(canvas, bgcolor);
  drawBackground(layerdict, false);
  drawHighlightsOnLayer(layerdict, false);

  // Save image
  var imgdata = canvas.toDataURL("image/png");

  var filename = pcbdata.metadata.title;
  if (pcbdata.metadata.revision) {
    filename += `.${pcbdata.metadata.revision}`;
  }
  filename += `.${layer}.png`;
  saveFile(filename, dataURLtoBlob(imgdata));
}

function saveSettings() {
  var data = {
    type: "InteractiveHtmlBom settings",
    version: 1,
    pcbmetadata: pcbdata.metadata,
    settings: settings,
  }
  var blob = new Blob([JSON.stringify(data, null, 4)], {
    type: "application/json"
  });
  saveFile(`${pcbdata.metadata.title}.settings.json`, blob);
}

function loadSettings() {
  var input = document.createElement("input");
  input.type = "file";
  input.accept = ".settings.json";
  input.onchange = function (e) {
    var file = e.target.files[0];
    var reader = new FileReader();
    reader.onload = readerEvent => {
      var content = readerEvent.target.result;
      var newSettings;
      try {
        newSettings = JSON.parse(content);
      } catch (e) {
        alert("Selected file is not InteractiveHtmlBom settings file.");
        return;
      }
      if (newSettings.type != "InteractiveHtmlBom settings") {
        alert("Selected file is not InteractiveHtmlBom settings file.");
        return;
      }
      var metadataMatches = newSettings.hasOwnProperty("pcbmetadata");
      if (metadataMatches) {
        for (var k in pcbdata.metadata) {
          if (!newSettings.pcbmetadata.hasOwnProperty(k) || newSettings.pcbmetadata[k] != pcbdata.metadata[k]) {
            metadataMatches = false;
          }
        }
      }
      if (!metadataMatches) {
        var currentMetadata = JSON.stringify(pcbdata.metadata, null, 4);
        var fileMetadata = JSON.stringify(newSettings.pcbmetadata, null, 4);
        if (!confirm(
          `Settins file metadata does not match current metadata.\n\n` +
          `Page metadata:\n${currentMetadata}\n\n` +
          `Settings file metadata:\n${fileMetadata}\n\n` +
          `Press OK if you would like to import settings anyway.`)) {
          return;
        }
      }
      overwriteSettings(newSettings.settings);
    }
    reader.readAsText(file, 'UTF-8');
  }
  input.click();
}

function resetSettings() {
  if (!confirm(
    `This will reset all checkbox states and other settings.\n\n` +
    `Press OK if you want to continue.`)) {
    return;
  }
  if (storage) {
    var keys = [];
    for (var i = 0; i < storage.length; i++) {
      var key = storage.key(i);
      if (key.startsWith(storagePrefix)) keys.push(key);
    }
    for (var key of keys) storage.removeItem(key);
  }
  location.reload();
}

function overwriteSettings(newSettings) {
  initDone = false;
  Object.assign(settings, newSettings);
  writeStorage("bomlayout", settings.bomlayout);
  writeStorage("bommode", settings.bommode);
  writeStorage("canvaslayout", settings.canvaslayout);
  writeStorage("bomCheckboxes", settings.checkboxes.join(","));
  document.getElementById("bomCheckboxes").value = settings.checkboxes.join(",");
  for (var checkbox of settings.checkboxes) {
    writeStorage("checkbox_" + checkbox, settings.checkboxStoredRefs[checkbox]);
  }
  writeStorage("markWhenChecked", settings.markWhenChecked);
  padsVisible(settings.renderPads);
  document.getElementById("padsCheckbox").checked = settings.renderPads;
  fabricationVisible(settings.renderFabrication);
  document.getElementById("fabricationCheckbox").checked = settings.renderFabrication;
  silkscreenVisible(settings.renderSilkscreen);
  document.getElementById("silkscreenCheckbox").checked = settings.renderSilkscreen;
  referencesVisible(settings.renderReferences);
  document.getElementById("referencesCheckbox").checked = settings.renderReferences;
  valuesVisible(settings.renderValues);
  document.getElementById("valuesCheckbox").checked = settings.renderValues;
  tracksVisible(settings.renderTracks);
  document.getElementById("tracksCheckbox").checked = settings.renderTracks;
  zonesVisible(settings.renderZones);
  document.getElementById("zonesCheckbox").checked = settings.renderZones;
  dnpOutline(settings.renderDnpOutline);
  document.getElementById("dnpOutlineCheckbox").checked = settings.renderDnpOutline;
  setRedrawOnDrag(settings.redrawOnDrag);
  document.getElementById("dragCheckbox").checked = settings.redrawOnDrag;
  setHighlightRowOnClick(settings.highlightRowOnClick);
  document.getElementById("highlightRowOnClickCheckbox").checked = settings.highlightRowOnClick;
  setDarkMode(settings.darkMode);
  document.getElementById("darkmodeCheckbox").checked = settings.darkMode;
  setHighlightPin1(settings.highlightpin1);
  document.forms.highlightpin1.highlightpin1.value = settings.highlightpin1;
  writeStorage("boardRotation", settings.boardRotation);
  document.getElementById("boardRotation").value = settings.boardRotation / 5;
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
  setOffsetBackRotation(settings.offsetBackRotation);
  document.getElementById("offsetBackRotationCheckbox").checked = settings.offsetBackRotation;
  initDone = true;
  prepCheckboxes();
  changeBomLayout(settings.bomlayout);
}

function saveFile(filename, blob) {
  var link = document.createElement("a");
  var objurl = URL.createObjectURL(blob);
  link.download = filename;
  link.href = objurl;
  link.click();
}

function dataURLtoBlob(dataurl) {
  var arr = dataurl.split(','),
    mime = arr[0].match(/:(.*?);/)[1],
    bstr = atob(arr[1]),
    n = bstr.length,
    u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new Blob([u8arr], {
    type: mime
  });
}

var settings = {
  canvaslayout: "FB",
  bomlayout: "left-right",
  bommode: "grouped",
  checkboxes: [],
  checkboxStoredRefs: {},
  darkMode: false,
  highlightpin1: "none",
  redrawOnDrag: true,
  boardRotation: 0,
  offsetBackRotation: false,
  renderPads: true,
  renderReferences: true,
  renderValues: true,
  renderSilkscreen: true,
  renderFabrication: true,
  renderDnpOutline: false,
  renderTracks: true,
  renderZones: true,
  columnOrder: [],
  hiddenColumns: [],
  netColors: {},
}

function initDefaults() {
  settings.bomlayout = readStorage("bomlayout");
  if (settings.bomlayout === null) {
    settings.bomlayout = config.bom_view;
  }
  if (!['bom-only', 'left-right', 'top-bottom'].includes(settings.bomlayout)) {
    settings.bomlayout = config.bom_view;
  }
  settings.bommode = readStorage("bommode");
  if (settings.bommode === null) {
    settings.bommode = "grouped";
  }
  if (settings.bommode == "netlist" && !pcbdata.nets) {
    settings.bommode = "grouped";
  }
  if (!["grouped", "ungrouped", "netlist"].includes(settings.bommode)) {
    settings.bommode = "grouped";
  }
  settings.canvaslayout = readStorage("canvaslayout");
  if (settings.canvaslayout === null) {
    settings.canvaslayout = config.layer_view;
  }
  var bomCheckboxes = readStorage("bomCheckboxes");
  if (bomCheckboxes === null) {
    bomCheckboxes = config.checkboxes;
  }
  settings.checkboxes = bomCheckboxes.split(",").filter((e) => e);
  document.getElementById("bomCheckboxes").value = bomCheckboxes;

  var highlightpin1 = readStorage("highlightpin1") || config.highlight_pin1;
  if (highlightpin1 === "false") highlightpin1 = "none";
  if (highlightpin1 === "true") highlightpin1 = "all";
  setHighlightPin1(highlightpin1);
  document.forms.highlightpin1.highlightpin1.value = highlightpin1;

  settings.markWhenChecked = readStorage("markWhenChecked") || "";
  populateMarkWhenCheckedOptions();

  function initBooleanSetting(storageString, def, elementId, func) {
    var b = readStorage(storageString);
    if (b === null) {
      b = def;
    } else {
      b = (b == "true");
    }
    document.getElementById(elementId).checked = b;
    func(b);
  }

  initBooleanSetting("padsVisible", config.show_pads, "padsCheckbox", padsVisible);
  initBooleanSetting("fabricationVisible", config.show_fabrication, "fabricationCheckbox", fabricationVisible);
  initBooleanSetting("silkscreenVisible", config.show_silkscreen, "silkscreenCheckbox", silkscreenVisible);
  initBooleanSetting("referencesVisible", true, "referencesCheckbox", referencesVisible);
  initBooleanSetting("valuesVisible", true, "valuesCheckbox", valuesVisible);
  if ("tracks" in pcbdata) {
    initBooleanSetting("tracksVisible", true, "tracksCheckbox", tracksVisible);
    initBooleanSetting("zonesVisible", true, "zonesCheckbox", zonesVisible);
  } else {
    document.getElementById("tracksAndZonesCheckboxes").style.display = "none";
    tracksVisible(false);
    zonesVisible(false);
  }
  initBooleanSetting("dnpOutline", false, "dnpOutlineCheckbox", dnpOutline);
  initBooleanSetting("redrawOnDrag", config.redraw_on_drag, "dragCheckbox", setRedrawOnDrag);
  initBooleanSetting("highlightRowOnClick", false, "highlightRowOnClickCheckbox", setHighlightRowOnClick);
  initBooleanSetting("darkmode", config.dark_mode, "darkmodeCheckbox", setDarkMode);

  var fields = ["checkboxes", "References"].concat(config.fields).concat(["Quantity"]);
  var hcols = JSON.parse(readStorage("hiddenColumns"));
  if (hcols === null) {
    hcols = [];
  }
  settings.hiddenColumns = hcols.filter(e => fields.includes(e));

  var cord = JSON.parse(readStorage("columnOrder"));
  if (cord === null) {
    cord = fields;
  } else {
    cord = cord.filter(e => fields.includes(e));
    if (cord.length != fields.length)
      cord = fields;
  }
  settings.columnOrder = cord;

  settings.boardRotation = readStorage("boardRotation");
  if (settings.boardRotation === null) {
    settings.boardRotation = config.board_rotation * 5;
  } else {
    settings.boardRotation = parseInt(settings.boardRotation);
  }
  document.getElementById("boardRotation").value = settings.boardRotation / 5;
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
  initBooleanSetting("offsetBackRotation", config.offset_back_rotation, "offsetBackRotationCheckbox", setOffsetBackRotation);

  settings.netColors = JSON.parse(readStorage("netColors")) || {};
}

// Helper classes for user js callbacks.

const IBOM_EVENT_TYPES = {
  ALL: "all",
  HIGHLIGHT_EVENT: "highlightEvent",
  CHECKBOX_CHANGE_EVENT: "checkboxChangeEvent",
  BOM_BODY_CHANGE_EVENT: "bomBodyChangeEvent",
}

const EventHandler = {
  callbacks: {},
  init: function () {
    for (eventType of Object.values(IBOM_EVENT_TYPES))
      this.callbacks[eventType] = [];
  },
  registerCallback: function (eventType, callback) {
    this.callbacks[eventType].push(callback);
  },
  emitEvent: function (eventType, eventArgs) {
    event = {
      eventType: eventType,
      args: eventArgs,
    }
    var callback;
    for (callback of this.callbacks[eventType])
      callback(event);
    for (callback of this.callbacks[IBOM_EVENT_TYPES.ALL])
      callback(event);
  }
}
EventHandler.init();

///////////////////////////////////////////////

///////////////////////////////////////////////
/* PCB rendering code */

var emptyContext2d = document.createElement("canvas").getContext("2d");

function deg2rad(deg) {
  return deg * Math.PI / 180;
}

function calcFontPoint(linepoint, text, offsetx, offsety, tilt) {
  var point = [
    linepoint[0] * text.width + offsetx,
    linepoint[1] * text.height + offsety
  ];
  // This approximates pcbnew behavior with how text tilts depending on horizontal justification
  point[0] -= (linepoint[1] + 0.5 * (1 + text.justify[0])) * text.height * tilt;
  return point;
}

function drawText(ctx, text, color) {
  if ("ref" in text && !settings.renderReferences) return;
  if ("val" in text && !settings.renderValues) return;
  ctx.save();
  ctx.fillStyle = color;
  ctx.strokeStyle = color;
  ctx.lineCap = "round";
  ctx.lineJoin = "round";
  ctx.lineWidth = text.thickness;
  if ("svgpath" in text) {
    ctx.stroke(new Path2D(text.svgpath));
    ctx.restore();
    return;
  }
  if ("polygons" in text) {
    ctx.fill(getPolygonsPath(text));
    ctx.restore();
    return;
  }
  ctx.translate(...text.pos);
  ctx.translate(text.thickness * 0.5, 0);
  var angle = -text.angle;
  if (text.attr.includes("mirrored")) {
    ctx.scale(-1, 1);
    angle = -angle;
  }
  var tilt = 0;
  if (text.attr.includes("italic")) {
    tilt = 0.125;
  }
  var interline = text.height * 1.5 + text.thickness;
  var txt = text.text.split("\n");
  // KiCad ignores last empty line.
  if (txt[txt.length - 1] == '') txt.pop();
  ctx.rotate(deg2rad(angle));
  var offsety = (1 - text.justify[1]) / 2 * text.height; // One line offset
  offsety -= (txt.length - 1) * (text.justify[1] + 1) / 2 * interline; // Multiline offset
  for (var i in txt) {
    var lineWidth = text.thickness + interline / 2 * tilt;
    for (var j = 0; j < txt[i].length; j++) {
      if (txt[i][j] == '\t') {
        var fourSpaces = 4 * pcbdata.font_data[' '].w * text.width;
        lineWidth += fourSpaces - lineWidth % fourSpaces;
      } else {
        if (txt[i][j] == '~') {
          j++;
          if (j == txt[i].length)
            break;
        }
        lineWidth += pcbdata.font_data[txt[i][j]].w * text.width;
      }
    }
    var offsetx = -lineWidth * (text.justify[0] + 1) / 2;
    var inOverbar = false;
    for (var j = 0; j < txt[i].length; j++) {
      if (config.kicad_text_formatting) {
        if (txt[i][j] == '\t') {
          var fourSpaces = 4 * pcbdata.font_data[' '].w * text.width;
          offsetx += fourSpaces - offsetx % fourSpaces;
          continue;
        } else if (txt[i][j] == '~') {
          j++;
          if (j == txt[i].length)
            break;
          if (txt[i][j] != '~') {
            inOverbar = !inOverbar;
          }
        }
      }
      var glyph = pcbdata.font_data[txt[i][j]];
      if (inOverbar) {
        var overbarStart = [offsetx, -text.height * 1.4 + offsety];
        var overbarEnd = [offsetx + text.width * glyph.w, overbarStart[1]];

        if (!lastHadOverbar) {
          overbarStart[0] += text.height * 1.4 * tilt;
          lastHadOverbar = true;
        }
        ctx.beginPath();
        ctx.moveTo(...overbarStart);
        ctx.lineTo(...overbarEnd);
        ctx.stroke();
      } else {
        lastHadOverbar = false;
      }
      for (var line of glyph.l) {
        ctx.beginPath();
        ctx.moveTo(...calcFontPoint(line[0], text, offsetx, offsety, tilt));
        for (var k = 1; k < line.length; k++) {
          ctx.lineTo(...calcFontPoint(line[k], text, offsetx, offsety, tilt));
        }
        ctx.stroke();
      }
      offsetx += glyph.w * text.width;
    }
    offsety += interline;
  }
  ctx.restore();
}

function drawedge(ctx, scalefactor, edge, color) {
  ctx.strokeStyle = color;
  ctx.fillStyle = color;
  ctx.lineWidth = Math.max(1 / scalefactor, edge.width);
  ctx.lineCap = "round";
  ctx.lineJoin = "round";
  if ("svgpath" in edge) {
    ctx.stroke(new Path2D(edge.svgpath));
  } else {
    ctx.beginPath();
    if (edge.type == "segment") {
      ctx.moveTo(...edge.start);
      ctx.lineTo(...edge.end);
    }
    if (edge.type == "rect") {
      ctx.moveTo(...edge.start);
      ctx.lineTo(edge.start[0], edge.end[1]);
      ctx.lineTo(...edge.end);
      ctx.lineTo(edge.end[0], edge.start[1]);
      ctx.lineTo(...edge.start);
    }
    if (edge.type == "arc") {
      ctx.arc(
        ...edge.start,
        edge.radius,
        deg2rad(edge.startangle),
        deg2rad(edge.endangle));
    }
    if (edge.type == "circle") {
      ctx.arc(
        ...edge.start,
        edge.radius,
        0, 2 * Math.PI);
      ctx.closePath();
    }
    if (edge.type == "curve") {
      ctx.moveTo(...edge.start);
      ctx.bezierCurveTo(...edge.cpa, ...edge.cpb, ...edge.end);
    }
    if("filled" in edge && edge.filled)
      ctx.fill();
    else
      ctx.stroke();
  }
}

function getChamferedRectPath(size, radius, chamfpos, chamfratio) {
  // chamfpos is a bitmask, left = 1, right = 2, bottom left = 4, bottom right = 8
  var path = new Path2D();
  var width = size[0];
  var height = size[1];
  var x = width * -0.5;
  var y = height * -0.5;
  var chamfOffset = Math.min(width, height) * chamfratio;
  path.moveTo(x, 0);
  if (chamfpos & 4) {
    path.lineTo(x, y + height - chamfOffset);
    path.lineTo(x + chamfOffset, y + height);
    path.lineTo(0, y + height);
  } else {
    path.arcTo(x, y + height, x + width, y + height, radius);
  }
  if (chamfpos & 8) {
    path.lineTo(x + width - chamfOffset, y + height);
    path.lineTo(x + width, y + height - chamfOffset);
    path.lineTo(x + width, 0);
  } else {
    path.arcTo(x + width, y + height, x + width, y, radius);
  }
  if (chamfpos & 2) {
    path.lineTo(x + width, y + chamfOffset);
    path.lineTo(x + width - chamfOffset, y);
    path.lineTo(0, y);
  } else {
    path.arcTo(x + width, y, x, y, radius);
  }
  if (chamfpos & 1) {
    path.lineTo(x + chamfOffset, y);
    path.lineTo(x, y + chamfOffset);
    path.lineTo(x, 0);
  } else {
    path.arcTo(x, y, x, y + height, radius);
  }
  path.closePath();
  return path;
}

function getOblongPath(size) {
  return getChamferedRectPath(size, Math.min(size[0], size[1]) / 2, 0, 0);
}

function getPolygonsPath(shape) {
  if (shape.path2d) {
    return shape.path2d;
  }
  if ("svgpath" in shape) {
    shape.path2d = new Path2D(shape.svgpath);
  } else {
    var path = new Path2D();
    for (var polygon of shape.polygons) {
      path.moveTo(...polygon[0]);
      for (var i = 1; i < polygon.length; i++) {
        path.lineTo(...polygon[i]);
      }
      path.closePath();
    }
    shape.path2d = path;
  }
  return shape.path2d;
}

function drawPolygonShape(ctx, scalefactor, shape, color) {
  ctx.save();
  if (!("svgpath" in shape)) {
    ctx.translate(...shape.pos);
    ctx.rotate(deg2rad(-shape.angle));
  }
  if("filled" in shape && !shape.filled) {
    ctx.strokeStyle = color;
    ctx.lineWidth = Math.max(1 / scalefactor, shape.width);
    ctx.lineCap = "round";
    ctx.lineJoin = "round";
    ctx.stroke(getPolygonsPath(shape));
  } else {
    ctx.fillStyle = color;
    ctx.fill(getPolygonsPath(shape));
  }
  ctx.restore();
}

function drawDrawing(ctx, scalefactor, drawing, color) {
  if (["segment", "arc", "circle", "curve", "rect"].includes(drawing.type)) {
    drawedge(ctx, scalefactor, drawing, color);
  } else if (drawing.type == "polygon") {
    drawPolygonShape(ctx, scalefactor, drawing, color);
  } else {
    drawText(ctx, drawing, color);
  }
}

function getCirclePath(radius) {
  var path = new Path2D();
  path.arc(0, 0, radius, 0, 2 * Math.PI);
  path.closePath();
  return path;
}

function getCachedPadPath(pad) {
  if (!pad.path2d) {
    // if path2d is not set, build one and cache it on pad object
    if (pad.shape == "rect") {
      pad.path2d = new Path2D();
      pad.path2d.rect(...pad.size.map(c => -c * 0.5), ...pad.size);
    } else if (pad.shape == "oval") {
      pad.path2d = getOblongPath(pad.size);
    } else if (pad.shape == "circle") {
      pad.path2d = getCirclePath(pad.size[0] / 2);
    } else if (pad.shape == "roundrect") {
      pad.path2d = getChamferedRectPath(pad.size, pad.radius, 0, 0);
    } else if (pad.shape == "chamfrect") {
      pad.path2d = getChamferedRectPath(pad.size, pad.radius, pad.chamfpos, pad.chamfratio)
    } else if (pad.shape == "custom") {
      pad.path2d = getPolygonsPath(pad);
    }
  }
  return pad.path2d;
}

function drawPad(ctx, pad, color, outline) {
  ctx.save();
  ctx.translate(...pad.pos);
  ctx.rotate(-deg2rad(pad.angle));
  if (pad.offset) {
    ctx.translate(...pad.offset);
  }
  ctx.fillStyle = color;
  ctx.strokeStyle = color;
  var path = getCachedPadPath(pad);
  if (outline) {
    ctx.stroke(path);
  } else {
    ctx.fill(path);
  }
  ctx.restore();
}

function drawPadHole(ctx, pad, padHoleColor) {
  if (pad.type != "th") return;
  ctx.save();
  ctx.translate(...pad.pos);
  ctx.rotate(-deg2rad(pad.angle));
  ctx.fillStyle = padHoleColor;
  if (pad.drillshape == "oblong") {
    ctx.fill(getOblongPath(pad.drillsize));
  } else if (pad.drillshape == "rect") {
    ctx.fill(getChamferedRectPath(pad.drillsize, 0, 0, 0));
  } else {
    ctx.fill(getCirclePath(pad.drillsize[0] / 2));
  }
  ctx.restore();
}

function drawFootprint(ctx, layer, scalefactor, footprint, colors, highlight, outline) {
  if (highlight) {
    // draw bounding box
    if (footprint.layer == layer) {
      ctx.save();
      ctx.globalAlpha = 0.2;
      ctx.translate(...footprint.bbox.pos);
      ctx.rotate(deg2rad(-footprint.bbox.angle));
      ctx.translate(...footprint.bbox.relpos);
      ctx.fillStyle = colors.pad;
      ctx.fillRect(0, 0, ...footprint.bbox.size);
      ctx.globalAlpha = 1;
      ctx.strokeStyle = colors.pad;
      ctx.lineWidth = 3 / scalefactor;
      ctx.strokeRect(0, 0, ...footprint.bbox.size);
      ctx.restore();
    }
  }
  // draw drawings
  for (var drawing of footprint.drawings) {
    if (drawing.layer == layer) {
      drawDrawing(ctx, scalefactor, drawing.drawing, colors.pad);
    }
  }
  ctx.lineWidth = 3 / scalefactor;
  // draw pads
  if (settings.renderPads) {
    for (var pad of footprint.pads) {
      if (pad.layers.includes(layer)) {
        drawPad(ctx, pad, colors.pad, outline);
        if (pad.pin1 &&
          (settings.highlightpin1 == "all" ||
            settings.highlightpin1 == "selected" && highlight)) {
          drawPad(ctx, pad, colors.outline, true);
        }
      }
    }
    for (var pad of footprint.pads) {
      drawPadHole(ctx, pad, colors.padHole);
    }
  }
}

function drawEdgeCuts(canvas, scalefactor) {
  var ctx = canvas.getContext("2d");
  var edgecolor = getComputedStyle(topmostdiv).getPropertyValue('--pcb-edge-color');
  for (var edge of pcbdata.edges) {
    drawDrawing(ctx, scalefactor, edge, edgecolor);
  }
}

function drawFootprints(canvas, layer, scalefactor, highlight) {
  var ctx = canvas.getContext("2d");
  ctx.lineWidth = 3 / scalefactor;
  var style = getComputedStyle(topmostdiv);

  var colors = {
    pad: style.getPropertyValue('--pad-color'),
    padHole: style.getPropertyValue('--pad-hole-color'),
    outline: style.getPropertyValue('--pin1-outline-color'),
  }

  for (var i = 0; i < pcbdata.footprints.length; i++) {
    var mod = pcbdata.footprints[i];
    var outline = settings.renderDnpOutline && pcbdata.bom.skipped.includes(i);
    var h = highlightedFootprints.includes(i);
    var d = markedFootprints.has(i);
    if (highlight) {
      if(h && d) {
        colors.pad = style.getPropertyValue('--pad-color-highlight-both');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight-both');
      } else if (h) {
        colors.pad = style.getPropertyValue('--pad-color-highlight');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight');
      } else if (d) {
        colors.pad = style.getPropertyValue('--pad-color-highlight-marked');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight-marked');
      }
    }
    if( h || d || !highlight) {
      drawFootprint(ctx, layer, scalefactor, mod, colors, highlight, outline);
    }
  }
}

function drawBgLayer(layername, canvas, layer, scalefactor, edgeColor, polygonColor, textColor) {
  var ctx = canvas.getContext("2d");
  for (var d of pcbdata.drawings[layername][layer]) {
    if (["segment", "arc", "circle", "curve", "rect"].includes(d.type)) {
      drawedge(ctx, scalefactor, d, edgeColor);
    } else if (d.type == "polygon") {
      drawPolygonShape(ctx, scalefactor, d, polygonColor);
    } else {
      drawText(ctx, d, textColor);
    }
  }
}

function drawTracks(canvas, layer, defaultColor, highlight) {
  ctx = canvas.getContext("2d");
  ctx.lineCap = "round";

  var hasHole = (track) => (
    'drillsize' in track &&
    track.start[0] == track.end[0] &&
    track.start[1] == track.end[1]);

  // First draw tracks and tented vias
  for (var track of pcbdata.tracks[layer]) {
    if (highlight && highlightedNet != track.net) continue;
    if (!hasHole(track)) {
      ctx.strokeStyle = highlight ? defaultColor : settings.netColors[track.net] || defaultColor;
      ctx.lineWidth = track.width;
      ctx.beginPath();
      if ('radius' in track) {
        ctx.arc(
          ...track.center,
          track.radius,
          deg2rad(track.startangle),
          deg2rad(track.endangle));
      } else {
        ctx.moveTo(...track.start);
        ctx.lineTo(...track.end);
      }
      ctx.stroke();
    }
  }
  // Second pass to draw untented vias
  var style = getComputedStyle(topmostdiv);
  var holeColor = style.getPropertyValue('--pad-hole-color')

  for (var track of pcbdata.tracks[layer]) {
    if (highlight && highlightedNet != track.net) continue;
    if (hasHole(track)) {
      ctx.strokeStyle = highlight ? defaultColor : settings.netColors[track.net] || defaultColor;
      ctx.lineWidth = track.width;
      ctx.beginPath();
      ctx.moveTo(...track.start);
      ctx.lineTo(...track.end);
      ctx.stroke();
      ctx.strokeStyle = holeColor;
      ctx.lineWidth = track.drillsize;
      ctx.lineTo(...track.end);
      ctx.stroke();
    }
  }
}

function drawZones(canvas, layer, defaultColor, highlight) {
  ctx = canvas.getContext("2d");
  ctx.lineJoin = "round";
  for (var zone of pcbdata.zones[layer]) {
    if (highlight && highlightedNet != zone.net) continue;
    ctx.strokeStyle = highlight ? defaultColor : settings.netColors[zone.net] || defaultColor;
    ctx.fillStyle = highlight ? defaultColor : settings.netColors[zone.net] || defaultColor;
    if (!zone.path2d) {
      zone.path2d = getPolygonsPath(zone);
    }
    ctx.fill(zone.path2d, zone.fillrule || "nonzero");
    if (zone.width > 0) {
      ctx.lineWidth = zone.width;
      ctx.stroke(zone.path2d);
    }
  }
}

function clearCanvas(canvas, color = null) {
  var ctx = canvas.getContext("2d");
  ctx.save();
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  if (color) {
    ctx.fillStyle = color;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
  } else {
    if (!window.matchMedia("print").matches)
      ctx.clearRect(0, 0, canvas.width, canvas.height);
  }
  ctx.restore();
}

function drawNets(canvas, layer, highlight) {
  var style = getComputedStyle(topmostdiv);
  if (settings.renderZones) {
    var zoneColor = style.getPropertyValue(highlight ? '--zone-color-highlight' : '--zone-color');
    drawZones(canvas, layer, zoneColor, highlight);
  }
  if (settings.renderTracks) {
    var trackColor = style.getPropertyValue(highlight ? '--track-color-highlight' : '--track-color');
    drawTracks(canvas, layer, trackColor, highlight);
  }
  if (highlight && settings.renderPads) {
    var padColor = style.getPropertyValue('--pad-color-highlight');
    var padHoleColor = style.getPropertyValue('--pad-hole-color');
    var ctx = canvas.getContext("2d");
    for (var footprint of pcbdata.footprints) {
      // draw pads
      var padDrawn = false;
      for (var pad of footprint.pads) {
        if (highlightedNet != pad.net) continue;
        if (pad.layers.includes(layer)) {
          drawPad(ctx, pad, padColor, false);
          padDrawn = true;
        }
      }
      if (padDrawn) {
        // redraw all pad holes because some pads may overlap
        for (var pad of footprint.pads) {
          drawPadHole(ctx, pad, padHoleColor);
        }
      }
    }
  }
}

function drawHighlightsOnLayer(canvasdict, clear = true) {
  if (clear) {
    clearCanvas(canvasdict.highlight);
  }
  if (markedFootprints.size > 0 || highlightedFootprints.length > 0) {
    drawFootprints(canvasdict.highlight, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom, true);
  }
  if (highlightedNet !== null) {
    drawNets(canvasdict.highlight, canvasdict.layer, true);
  }
}

function drawHighlights() {
  drawHighlightsOnLayer(allcanvas.front);
  drawHighlightsOnLayer(allcanvas.back);
}

function drawBackground(canvasdict, clear = true) {
  if (clear) {
    clearCanvas(canvasdict.bg);
    clearCanvas(canvasdict.fab);
    clearCanvas(canvasdict.silk);
  }

  drawNets(canvasdict.bg, canvasdict.layer, false);
  drawFootprints(canvasdict.bg, canvasdict.layer,
    canvasdict.transform.s * canvasdict.transform.zoom, false);

  drawEdgeCuts(canvasdict.bg, canvasdict.transform.s * canvasdict.transform.zoom);

  var style = getComputedStyle(topmostdiv);
  var edgeColor = style.getPropertyValue('--silkscreen-edge-color');
  var polygonColor = style.getPropertyValue('--silkscreen-polygon-color');
  var textColor = style.getPropertyValue('--silkscreen-text-color');
  if (settings.renderSilkscreen) {
    drawBgLayer(
      "silkscreen", canvasdict.silk, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom,
      edgeColor, polygonColor, textColor);
  }
  edgeColor = style.getPropertyValue('--fabrication-edge-color');
  polygonColor = style.getPropertyValue('--fabrication-polygon-color');
  textColor = style.getPropertyValue('--fabrication-text-color');
  if (settings.renderFabrication) {
    drawBgLayer(
      "fabrication", canvasdict.fab, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom,
      edgeColor, polygonColor, textColor);
  }
}

function prepareCanvas(canvas, flip, transform) {
  var ctx = canvas.getContext("2d");
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  ctx.scale(transform.zoom, transform.zoom);
  ctx.translate(transform.panx, transform.pany);
  if (flip) {
    ctx.scale(-1, 1);
  }
  ctx.translate(transform.x, transform.y);
  ctx.rotate(deg2rad(settings.boardRotation + (flip && settings.offsetBackRotation ? - 180 : 0)));
  ctx.scale(transform.s, transform.s);
}

function prepareLayer(canvasdict) {
  var flip = (canvasdict.layer === "B");
  for (var c of ["bg", "fab", "silk", "highlight"]) {
    prepareCanvas(canvasdict[c], flip, canvasdict.transform);
  }
}

function rotateVector(v, angle) {
  angle = deg2rad(angle);
  return [
    v[0] * Math.cos(angle) - v[1] * Math.sin(angle),
    v[0] * Math.sin(angle) + v[1] * Math.cos(angle)
  ];
}

function applyRotation(bbox, flip) {
  var corners = [
    [bbox.minx, bbox.miny],
    [bbox.minx, bbox.maxy],
    [bbox.maxx, bbox.miny],
    [bbox.maxx, bbox.maxy],
  ];
  corners = corners.map((v) => rotateVector(v, settings.boardRotation + (flip && settings.offsetBackRotation ? - 180 : 0)));
  return {
    minx: corners.reduce((a, v) => Math.min(a, v[0]), Infinity),
    miny: corners.reduce((a, v) => Math.min(a, v[1]), Infinity),
    maxx: corners.reduce((a, v) => Math.max(a, v[0]), -Infinity),
    maxy: corners.reduce((a, v) => Math.max(a, v[1]), -Infinity),
  }
}

function recalcLayerScale(layerdict, width, height) {
  var flip = (layerdict.layer === "B");
  var bbox = applyRotation(pcbdata.edges_bbox, flip);
  var scalefactor = 0.98 * Math.min(
    width / (bbox.maxx - bbox.minx),
    height / (bbox.maxy - bbox.miny)
  );
  if (scalefactor < 0.1) {
    scalefactor = 1;
  }
  layerdict.transform.s = scalefactor;
  if (flip) {
    layerdict.transform.x = -((bbox.maxx + bbox.minx) * scalefactor + width) * 0.5;
  } else {
    layerdict.transform.x = -((bbox.maxx + bbox.minx) * scalefactor - width) * 0.5;
  }
  layerdict.transform.y = -((bbox.maxy + bbox.miny) * scalefactor - height) * 0.5;
  for (var c of ["bg", "fab", "silk", "highlight"]) {
    canvas = layerdict[c];
    canvas.width = width;
    canvas.height = height;
    canvas.style.width = (width / devicePixelRatio) + "px";
    canvas.style.height = (height / devicePixelRatio) + "px";
  }
}

function redrawCanvas(layerdict) {
  prepareLayer(layerdict);
  drawBackground(layerdict);
  drawHighlightsOnLayer(layerdict);
}

function resizeCanvas(layerdict) {
  var canvasdivid = {
    "F": "frontcanvas",
    "B": "backcanvas"
  } [layerdict.layer];
  var width = document.getElementById(canvasdivid).clientWidth * devicePixelRatio;
  var height = document.getElementById(canvasdivid).clientHeight * devicePixelRatio;
  recalcLayerScale(layerdict, width, height);
  redrawCanvas(layerdict);
}

function resizeAll() {
  resizeCanvas(allcanvas.front);
  resizeCanvas(allcanvas.back);
}

function pointWithinDistanceToSegment(x, y, x1, y1, x2, y2, d) {
  var A = x - x1;
  var B = y - y1;
  var C = x2 - x1;
  var D = y2 - y1;

  var dot = A * C + B * D;
  var len_sq = C * C + D * D;
  var dx, dy;
  if (len_sq == 0) {
    // start and end of the segment coincide
    dx = x - x1;
    dy = y - y1;
  } else {
    var param = dot / len_sq;
    var xx, yy;
    if (param < 0) {
      xx = x1;
      yy = y1;
    } else if (param > 1) {
      xx = x2;
      yy = y2;
    } else {
      xx = x1 + param * C;
      yy = y1 + param * D;
    }
    dx = x - xx;
    dy = y - yy;
  }
  return dx * dx + dy * dy <= d * d;
}

function modulo(n, mod) {
  return ((n % mod) + mod) % mod;
}

function pointWithinDistanceToArc(x, y, xc, yc, radius, startangle, endangle, d) {
  var dx = x - xc;
  var dy = y - yc;
  var r_sq = dx * dx + dy * dy;
  var rmin = Math.max(0, radius - d);
  var rmax = radius + d;

  if (r_sq < rmin * rmin || r_sq > rmax * rmax)
    return false;

  var angle1 = modulo(deg2rad(startangle), 2 * Math.PI);
  var dx1 = xc + radius * Math.cos(angle1) - x;
  var dy1 = yc + radius * Math.sin(angle1) - y;
  if (dx1 * dx1 + dy1 * dy1 <= d * d)
    return true;

  var angle2 = modulo(deg2rad(endangle), 2 * Math.PI);
  var dx2 = xc + radius * Math.cos(angle2) - x;
  var dy2 = yc + radius * Math.sin(angle2) - y;
  if (dx2 * dx2 + dy2 * dy2 <= d * d)
    return true;

  var angle = modulo(Math.atan2(dy, dx), 2 * Math.PI);
  if (angle1 > angle2)
    return (angle >= angle2 || angle <= angle1);
  else
    return (angle >= angle1 && angle <= angle2);
}

function pointWithinPad(x, y, pad) {
  var v = [x - pad.pos[0], y - pad.pos[1]];
  v = rotateVector(v, pad.angle);
  if (pad.offset) {
    v[0] -= pad.offset[0];
    v[1] -= pad.offset[1];
  }
  return emptyContext2d.isPointInPath(getCachedPadPath(pad), ...v);
}

function netHitScan(layer, x, y) {
  // Check track segments
  if (settings.renderTracks && pcbdata.tracks) {
    for (var track of pcbdata.tracks[layer]) {
      if ('radius' in track) {
        if (pointWithinDistanceToArc(x, y, ...track.center, track.radius, track.startangle, track.endangle, track.width / 2)) {
          return track.net;
        }
      } else {
        if (pointWithinDistanceToSegment(x, y, ...track.start, ...track.end, track.width / 2)) {
          return track.net;
        }
      }
    }
  }
  // Check pads
  if (settings.renderPads) {
    for (var footprint of pcbdata.footprints) {
      for (var pad of footprint.pads) {
        if (pad.layers.includes(layer) && pointWithinPad(x, y, pad)) {
          return pad.net;
        }
      }
    }
  }
  return null;
}

function pointWithinFootprintBbox(x, y, bbox) {
  var v = [x - bbox.pos[0], y - bbox.pos[1]];
  v = rotateVector(v, bbox.angle);
  return bbox.relpos[0] <= v[0] && v[0] <= bbox.relpos[0] + bbox.size[0] &&
    bbox.relpos[1] <= v[1] && v[1] <= bbox.relpos[1] + bbox.size[1];
}

function bboxHitScan(layer, x, y) {
  var result = [];
  for (var i = 0; i < pcbdata.footprints.length; i++) {
    var footprint = pcbdata.footprints[i];
    if (footprint.layer == layer) {
      if (pointWithinFootprintBbox(x, y, footprint.bbox)) {
        result.push(i);
      }
    }
  }
  return result;
}

function handlePointerDown(e, layerdict) {
  if (e.button != 0 && e.button != 1) {
    return;
  }
  e.preventDefault();
  e.stopPropagation();

  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  layerdict.pointerStates[e.pointerId] = {
    distanceTravelled: 0,
    lastX: e.offsetX,
    lastY: e.offsetY,
    downTime: Date.now(),
  };
}

function handleMouseClick(e, layerdict) {
  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  var x = e.offsetX;
  var y = e.offsetY;
  var t = layerdict.transform;
  var flip = layerdict.layer === "B";
  if (flip) {
    x = (devicePixelRatio * x / t.zoom - t.panx + t.x) / -t.s;
  } else {
    x = (devicePixelRatio * x / t.zoom - t.panx - t.x) / t.s;
  }
  y = (devicePixelRatio * y / t.zoom - t.y - t.pany) / t.s;
  var v = rotateVector([x, y], -settings.boardRotation + (flip && settings.offsetBackRotation ? - 180 : 0));
  if ("nets" in pcbdata) {
    var net = netHitScan(layerdict.layer, ...v);
    if (net !== highlightedNet) {
      netClicked(net);
    }
  }
  if (highlightedNet === null) {
    var footprints = bboxHitScan(layerdict.layer, ...v);
    if (footprints.length > 0) {
      footprintsClicked(footprints);
    }
  }
}

function handlePointerLeave(e, layerdict) {
  e.preventDefault();
  e.stopPropagation();

  if (!settings.redrawOnDrag) {
    redrawCanvas(layerdict);
  }

  delete layerdict.pointerStates[e.pointerId];
}

function resetTransform(layerdict) {
  layerdict.transform.panx = 0;
  layerdict.transform.pany = 0;
  layerdict.transform.zoom = 1;
  redrawCanvas(layerdict);
}

function handlePointerUp(e, layerdict) {
  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  e.preventDefault();
  e.stopPropagation();

  if (e.button == 2) {
    // Reset pan and zoom on right click.
    resetTransform(layerdict);
    layerdict.anotherPointerTapped = false;
    return;
  }

  // We haven't necessarily had a pointermove event since the interaction started, so make sure we update this now
  var ptr = layerdict.pointerStates[e.pointerId];
  ptr.distanceTravelled += Math.abs(e.offsetX - ptr.lastX) + Math.abs(e.offsetY - ptr.lastY);

  if (e.button == 0 && ptr.distanceTravelled < 10 && Date.now() - ptr.downTime <= 500) {
    if (Object.keys(layerdict.pointerStates).length == 1) {
      if (layerdict.anotherPointerTapped) {
        // This is the second pointer coming off of a two-finger tap
        resetTransform(layerdict);
      } else {
        // This is just a regular tap
        handleMouseClick(e, layerdict);
      }
      layerdict.anotherPointerTapped = false;
    } else {
      // This is the first finger coming off of what could become a two-finger tap
      layerdict.anotherPointerTapped = true;
    }
  } else {
    if (!settings.redrawOnDrag) {
      redrawCanvas(layerdict);
    }
    layerdict.anotherPointerTapped = false;
  }

  delete layerdict.pointerStates[e.pointerId];
}

function handlePointerMove(e, layerdict) {
  if (!layerdict.pointerStates.hasOwnProperty(e.pointerId)) {
    return;
  }
  e.preventDefault();
  e.stopPropagation();

  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  var thisPtr = layerdict.pointerStates[e.pointerId];

  var dx = e.offsetX - thisPtr.lastX;
  var dy = e.offsetY - thisPtr.lastY;

  // If this number is low on pointer up, we count the action as a click
  thisPtr.distanceTravelled += Math.abs(dx) + Math.abs(dy);

  if (Object.keys(layerdict.pointerStates).length == 1) {
    // This is a simple drag
    layerdict.transform.panx += devicePixelRatio * dx / layerdict.transform.zoom;
    layerdict.transform.pany += devicePixelRatio * dy / layerdict.transform.zoom;
  } else if (Object.keys(layerdict.pointerStates).length == 2) {
    var otherPtr = Object.values(layerdict.pointerStates).filter((ptr) => ptr != thisPtr)[0];

    var oldDist = Math.sqrt(Math.pow(thisPtr.lastX - otherPtr.lastX, 2) + Math.pow(thisPtr.lastY - otherPtr.lastY, 2));
    var newDist = Math.sqrt(Math.pow(e.offsetX - otherPtr.lastX, 2) + Math.pow(e.offsetY - otherPtr.lastY, 2));

    var scaleFactor = newDist / oldDist;

    if (scaleFactor != NaN) {
      layerdict.transform.zoom *= scaleFactor;

      var zoomd = (1 - scaleFactor) / layerdict.transform.zoom;
      layerdict.transform.panx += devicePixelRatio * otherPtr.lastX * zoomd;
      layerdict.transform.pany += devicePixelRatio * otherPtr.lastY * zoomd;
    }
  }

  thisPtr.lastX = e.offsetX;
  thisPtr.lastY = e.offsetY;

  if (settings.redrawOnDrag) {
    redrawCanvas(layerdict);
  }
}

function handleMouseWheel(e, layerdict) {
  e.preventDefault();
  e.stopPropagation();
  var t = layerdict.transform;
  var wheeldelta = e.deltaY;
  if (e.deltaMode == 1) {
    // FF only, scroll by lines
    wheeldelta *= 30;
  } else if (e.deltaMode == 2) {
    wheeldelta *= 300;
  }
  var m = Math.pow(1.1, -wheeldelta / 40);
  // Limit amount of zoom per tick.
  if (m > 2) {
    m = 2;
  } else if (m < 0.5) {
    m = 0.5;
  }
  t.zoom *= m;
  var zoomd = (1 - m) / t.zoom;
  t.panx += devicePixelRatio * e.offsetX * zoomd;
  t.pany += devicePixelRatio * e.offsetY * zoomd;
  redrawCanvas(layerdict);
}

function addMouseHandlers(div, layerdict) {
  div.addEventListener("pointerdown", function(e) {
    handlePointerDown(e, layerdict);
  });
  div.addEventListener("pointermove", function(e) {
    handlePointerMove(e, layerdict);
  });
  div.addEventListener("pointerup", function(e) {
    handlePointerUp(e, layerdict);
  });
  var pointerleave = function(e) {
    handlePointerLeave(e, layerdict);
  }
  div.addEventListener("pointercancel", pointerleave);
  div.addEventListener("pointerleave", pointerleave);
  div.addEventListener("pointerout", pointerleave);

  div.onwheel = function(e) {
    handleMouseWheel(e, layerdict);
  }
  for (var element of [div, layerdict.bg, layerdict.fab, layerdict.silk, layerdict.highlight]) {
    element.addEventListener("contextmenu", function(e) {
      e.preventDefault();
    }, false);
  }
}

function setRedrawOnDrag(value) {
  settings.redrawOnDrag = value;
  writeStorage("redrawOnDrag", value);
}

function setBoardRotation(value) {
  settings.boardRotation = value * 5;
  writeStorage("boardRotation", settings.boardRotation);
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
  resizeAll();
}

function setOffsetBackRotation(value) {
  settings.offsetBackRotation = value;
  writeStorage("offsetBackRotation", value);
  resizeAll();
}

function initRender() {
  allcanvas = {
    front: {
      transform: {
        x: 0,
        y: 0,
        s: 1,
        panx: 0,
        pany: 0,
        zoom: 1,
      },
      pointerStates: {},
      anotherPointerTapped: false,
      bg: document.getElementById("F_bg"),
      fab: document.getElementById("F_fab"),
      silk: document.getElementById("F_slk"),
      highlight: document.getElementById("F_hl"),
      layer: "F",
    },
    back: {
      transform: {
        x: 0,
        y: 0,
        s: 1,
        panx: 0,
        pany: 0,
        zoom: 1,
      },
      pointerStates: {},
      anotherPointerTapped: false,
      bg: document.getElementById("B_bg"),
      fab: document.getElementById("B_fab"),
      silk: document.getElementById("B_slk"),
      highlight: document.getElementById("B_hl"),
      layer: "B",
    }
  };
  addMouseHandlers(document.getElementById("frontcanvas"), allcanvas.front);
  addMouseHandlers(document.getElementById("backcanvas"), allcanvas.back);
}

///////////////////////////////////////////////

///////////////////////////////////////////////
/*
 * Table reordering via Drag'n'Drop
 * Inspired by: https://htmldom.dev/drag-and-drop-table-column
 */

function setBomHandlers() {

  const bom = document.getElementById('bomtable');

  let dragName;
  let placeHolderElements;
  let draggingElement;
  let forcePopulation;
  let xOffset;
  let yOffset;
  let wasDragged;

  const mouseUpHandler = function(e) {
    // Delete dragging element
    draggingElement.remove();

    // Make BOM selectable again
    bom.style.removeProperty("userSelect");

    // Remove listeners
    document.removeEventListener('mousemove', mouseMoveHandler);
    document.removeEventListener('mouseup', mouseUpHandler);

    if (wasDragged) {
      // Redraw whole BOM
      populateBomTable();
    }
  }

  const mouseMoveHandler = function(e) {
    // Notice the dragging
    wasDragged = true;

    // Make the dragged element visible
    draggingElement.style.removeProperty("display");

    // Set elements position to mouse position
    draggingElement.style.left = `${e.screenX - xOffset}px`;
    draggingElement.style.top = `${e.screenY - yOffset}px`;

    // Forced redrawing of BOM table
    if (forcePopulation) {
      forcePopulation = false;
      // Copy array
      phe = Array.from(placeHolderElements);
      // populate BOM table again
      populateBomHeader(dragName, phe);
      populateBomBody(dragName, phe);
    }

    // Set up array of hidden columns
    var hiddenColumns = Array.from(settings.hiddenColumns);
    // In the ungrouped mode, quantity don't exist
    if (settings.bommode === "ungrouped")
      hiddenColumns.push("Quantity");
    // If no checkbox fields can be found, we consider them hidden
    if (settings.checkboxes.length == 0)
      hiddenColumns.push("checkboxes");

    // Get table headers and group them into checkboxes, extrafields and normal headers
    const bh = document.getElementById("bomhead");
    headers = Array.from(bh.querySelectorAll("th"))
    headers.shift() // numCol is not part of the columnOrder
    headerGroups = []
    lastCompoundClass = null;
    for (i = 0; i < settings.columnOrder.length; i++) {
      cElem = settings.columnOrder[i];
      if (hiddenColumns.includes(cElem)) {
        // Hidden columns appear as a dummy element
        headerGroups.push([]);
        continue;
      }
      elem = headers.filter(e => getColumnOrderName(e) === cElem)[0];
      if (elem.classList.contains("bom-checkbox")) {
        if (lastCompoundClass === "bom-checkbox") {
          cbGroup = headerGroups.pop();
          cbGroup.push(elem);
          headerGroups.push(cbGroup);
        } else {
          lastCompoundClass = "bom-checkbox";
          headerGroups.push([elem])
        }
      } else {
        headerGroups.push([elem])
      }
    }

    // Copy settings.columnOrder
    var columns = Array.from(settings.columnOrder)

    // Set up array with indices of hidden columns
    var hiddenIndices = hiddenColumns.map(e => settings.columnOrder.indexOf(e));
    var dragIndex = columns.indexOf(dragName);
    var swapIndex = dragIndex;
    var swapDone = false;

    // Check if the current dragged element is swapable with the left or right element
    if (dragIndex > 0) {
      // Get left headers boundingbox
      swapIndex = dragIndex - 1;
      while (hiddenIndices.includes(swapIndex) && swapIndex > 0)
        swapIndex--;
      if (!hiddenIndices.includes(swapIndex)) {
        box = getBoundingClientRectFromMultiple(headerGroups[swapIndex]);
        if (e.clientX < box.left + window.scrollX + (box.width / 2)) {
          swapElement = columns[dragIndex];
          columns.splice(dragIndex, 1);
          columns.splice(swapIndex, 0, swapElement);
          forcePopulation = true;
          swapDone = true;
        }
      }
    }
    if ((!swapDone) && dragIndex < headerGroups.length - 1) {
      // Get right headers boundingbox
      swapIndex = dragIndex + 1;
      while (hiddenIndices.includes(swapIndex))
        swapIndex++;
      if (swapIndex < headerGroups.length) {
        box = getBoundingClientRectFromMultiple(headerGroups[swapIndex]);
        if (e.clientX > box.left + window.scrollX + (box.width / 2)) {
          swapElement = columns[dragIndex];
          columns.splice(dragIndex, 1);
          columns.splice(swapIndex, 0, swapElement);
          forcePopulation = true;
          swapDone = true;
        }
      }
    }

    // Write back change to storage
    if (swapDone) {
      settings.columnOrder = columns
      writeStorage("columnOrder", JSON.stringify(columns));
    }

  }

  const mouseDownHandler = function(e) {
    var target = e.target;
    if (target.tagName.toLowerCase() != "td")
      target = target.parentElement;

    // Used to check if a dragging has ever happened
    wasDragged = false;

    // Create new element which will be displayed as the dragged column
    draggingElement = document.createElement("div")
    draggingElement.classList.add("dragging");
    draggingElement.style.display = "none";
    draggingElement.style.position = "absolute";
    draggingElement.style.overflow = "hidden";

    // Get bomhead and bombody elements
    const bh = document.getElementById("bomhead");
    const bb = document.getElementById("bombody");

    // Get all compound headers for the current column
    var compoundHeaders;
    if (target.classList.contains("bom-checkbox")) {
      compoundHeaders = Array.from(bh.querySelectorAll("th.bom-checkbox"));
    } else {
      compoundHeaders = [target];
    }

    // Create new table which will display the column
    var newTable = document.createElement("table");
    newTable.classList.add("bom");
    newTable.style.background = "white";
    draggingElement.append(newTable);

    // Create new header element
    var newHeader = document.createElement("thead");
    newTable.append(newHeader);

    // Set up array for storing all placeholder elements
    placeHolderElements = [];

    // Add all compound headers to the new thead element and placeholders
    compoundHeaders.forEach(function(h) {
      clone = cloneElementWithDimensions(h);
      newHeader.append(clone);
      placeHolderElements.push(clone);
    });

    // Create new body element
    var newBody = document.createElement("tbody");
    newTable.append(newBody);

    // Get indices for compound headers
    var idxs = compoundHeaders.map(e => getBomTableHeaderIndex(e));

    // For each row in the BOM body...
    var rows = bb.querySelectorAll("tr");
    rows.forEach(function(row) {
      // ..get the cells for the compound column
      const tds = row.querySelectorAll("td");
      var copytds = idxs.map(i => tds[i]);
      // Add them to the new element and the placeholders
      var newRow = document.createElement("tr");
      copytds.forEach(function(td) {
        clone = cloneElementWithDimensions(td);
        newRow.append(clone);
        placeHolderElements.push(clone);
      });
      newBody.append(newRow);
    });

    // Compute width for compound header
    var width = compoundHeaders.reduce((acc, x) => acc + x.clientWidth, 0);
    draggingElement.style.width = `${width}px`;

    // Insert the new dragging element and disable selection on BOM
    bom.insertBefore(draggingElement, null);
    bom.style.userSelect = "none";

    // Determine the mouse position offset
    xOffset = e.screenX - compoundHeaders.reduce((acc, x) => Math.min(acc, x.offsetLeft), compoundHeaders[0].offsetLeft);
    yOffset = e.screenY - compoundHeaders[0].offsetTop;

    // Get name for the column in settings.columnOrder
    dragName = getColumnOrderName(target);

    // Change text and class for placeholder elements
    placeHolderElements = placeHolderElements.map(function(e) {
      newElem = cloneElementWithDimensions(e);
      newElem.textContent = "";
      newElem.classList.add("placeholder");
      return newElem;
    });

    // On next mouse move, the whole BOM needs to be redrawn to show the placeholders
    forcePopulation = true;

    // Add listeners for move and up on mouse
    document.addEventListener('mousemove', mouseMoveHandler);
    document.addEventListener('mouseup', mouseUpHandler);
  }

  // In netlist mode, there is nothing to reorder
  if (settings.bommode === "netlist")
    return;

  // Add mouseDownHandler to every column except the numCol
  bom.querySelectorAll("th")
    .forEach(function(head) {
      if (!head.classList.contains("numCol")) {
        head.onmousedown = mouseDownHandler;
      }
    });

}

function getBoundingClientRectFromMultiple(elements) {
  var elems = Array.from(elements);

  if (elems.length == 0)
    return null;

  var box = elems.shift()
    .getBoundingClientRect();

  elems.forEach(function(elem) {
    var elembox = elem.getBoundingClientRect();
    box.left = Math.min(elembox.left, box.left);
    box.top = Math.min(elembox.top, box.top);
    box.width += elembox.width;
    box.height = Math.max(elembox.height, box.height);
  });

  return box;
}

function cloneElementWithDimensions(elem) {
  var newElem = elem.cloneNode(true);
  newElem.style.height = window.getComputedStyle(elem).height;
  newElem.style.width = window.getComputedStyle(elem).width;
  return newElem;
}

function getBomTableHeaderIndex(elem) {
  const bh = document.getElementById('bomhead');
  const ths = Array.from(bh.querySelectorAll("th"));
  return ths.indexOf(elem);
}

function getColumnOrderName(elem) {
  var cname = elem.getAttribute("col_name");
  if (cname === "bom-checkbox")
    return "checkboxes";
  else
    return cname;
}

function resizableGrid(tablehead) {
  var cols = tablehead.firstElementChild.children;
  var rowWidth = tablehead.offsetWidth;

  for (var i = 1; i < cols.length; i++) {
    if (cols[i].classList.contains("bom-checkbox"))
      continue;
    cols[i].style.width = ((cols[i].clientWidth - paddingDiff(cols[i])) * 100 / rowWidth) + '%';
  }

  for (var i = 1; i < cols.length - 1; i++) {
    var div = document.createElement('div');
    div.className = "column-width-handle";
    cols[i].appendChild(div);
    setListeners(div);
  }

  function setListeners(div) {
    var startX, curCol, nxtCol, curColWidth, nxtColWidth, rowWidth;

    div.addEventListener('mousedown', function(e) {
      e.preventDefault();
      e.stopPropagation();

      curCol = e.target.parentElement;
      nxtCol = curCol.nextElementSibling;
      startX = e.pageX;

      var padding = paddingDiff(curCol);

      rowWidth = curCol.parentElement.offsetWidth;
      curColWidth = curCol.clientWidth - padding;
      nxtColWidth = nxtCol.clientWidth - padding;
    });

    document.addEventListener('mousemove', function(e) {
      if (startX) {
        var diffX = e.pageX - startX;
        diffX = -Math.min(-diffX, curColWidth - 20);
        diffX = Math.min(diffX, nxtColWidth - 20);

        curCol.style.width = ((curColWidth + diffX) * 100 / rowWidth) + '%';
        nxtCol.style.width = ((nxtColWidth - diffX) * 100 / rowWidth) + '%';
        console.log(`${curColWidth + nxtColWidth} ${(curColWidth + diffX) * 100 / rowWidth + (nxtColWidth - diffX) * 100 / rowWidth}`);
      }
    });

    document.addEventListener('mouseup', function(e) {
      curCol = undefined;
      nxtCol = undefined;
      startX = undefined;
      nxtColWidth = undefined;
      curColWidth = undefined
    });
  }

  function paddingDiff(col) {

    if (getStyleVal(col, 'box-sizing') == 'border-box') {
      return 0;
    }

    var padLeft = getStyleVal(col, 'padding-left');
    var padRight = getStyleVal(col, 'padding-right');
    return (parseInt(padLeft) + parseInt(padRight));

  }

  function getStyleVal(elm, css) {
    return (window.getComputedStyle(elm, null).getPropertyValue(css))
  }
}

///////////////////////////////////////////////

///////////////////////////////////////////////
/* DOM manipulation and misc code */

var bomsplit;
var canvassplit;
var initDone = false;
var bomSortFunction = null;
var currentSortColumn = null;
var currentSortOrder = null;
var currentHighlightedRowId;
var highlightHandlers = [];
var footprintIndexToHandler = {};
var netsToHandler = {};
var markedFootprints = new Set();
var highlightedFootprints = [];
var highlightedNet = null;
var lastClicked;

function dbg(html) {
  dbgdiv.innerHTML = html;
}

function redrawIfInitDone() {
  if (initDone) {
    redrawCanvas(allcanvas.front);
    redrawCanvas(allcanvas.back);
  }
}

function padsVisible(value) {
  writeStorage("padsVisible", value);
  settings.renderPads = value;
  redrawIfInitDone();
}

function referencesVisible(value) {
  writeStorage("referencesVisible", value);
  settings.renderReferences = value;
  redrawIfInitDone();
}

function valuesVisible(value) {
  writeStorage("valuesVisible", value);
  settings.renderValues = value;
  redrawIfInitDone();
}

function tracksVisible(value) {
  writeStorage("tracksVisible", value);
  settings.renderTracks = value;
  redrawIfInitDone();
}

function zonesVisible(value) {
  writeStorage("zonesVisible", value);
  settings.renderZones = value;
  redrawIfInitDone();
}

function dnpOutline(value) {
  writeStorage("dnpOutline", value);
  settings.renderDnpOutline = value;
  redrawIfInitDone();
}

function setDarkMode(value) {
  if (value) {
    topmostdiv.classList.add("dark");
  } else {
    topmostdiv.classList.remove("dark");
  }
  writeStorage("darkmode", value);
  settings.darkMode = value;
  redrawIfInitDone();
  if (initDone) {
    populateBomTable();
  }
}

function setShowBOMColumn(field, value) {
  if (field === "references") {
    var rl = document.getElementById("reflookup");
    rl.disabled = !value;
    if (!value) {
      rl.value = "";
      updateRefLookup("");
    }
  }

  var n = settings.hiddenColumns.indexOf(field);
  if (value) {
    if (n != -1) {
      settings.hiddenColumns.splice(n, 1);
    }
  } else {
    if (n == -1) {
      settings.hiddenColumns.push(field);
    }
  }

  writeStorage("hiddenColumns", JSON.stringify(settings.hiddenColumns));

  if (initDone) {
    populateBomTable();
  }

  redrawIfInitDone();
}


function setFullscreen(value) {
  if (value) {
    document.documentElement.requestFullscreen();
  } else {
    document.exitFullscreen();
  }
}

function fabricationVisible(value) {
  writeStorage("fabricationVisible", value);
  settings.renderFabrication = value;
  redrawIfInitDone();
}

function silkscreenVisible(value) {
  writeStorage("silkscreenVisible", value);
  settings.renderSilkscreen = value;
  redrawIfInitDone();
}

function setHighlightPin1(value) {
  writeStorage("highlightpin1", value);
  settings.highlightpin1 = value;
  redrawIfInitDone();
}

function setHighlightRowOnClick(value) {
  settings.highlightRowOnClick = value;
  writeStorage("highlightRowOnClick", value);
  if (initDone) {
    populateBomTable();
  }
}

function getStoredCheckboxRefs(checkbox) {
  function convert(ref) {
    var intref = parseInt(ref);
    if (isNaN(intref)) {
      for (var i = 0; i < pcbdata.footprints.length; i++) {
        if (pcbdata.footprints[i].ref == ref) {
          return i;
        }
      }
      return -1;
    } else {
      return intref;
    }
  }
  if (!(checkbox in settings.checkboxStoredRefs)) {
    var val = readStorage("checkbox_" + checkbox);
    settings.checkboxStoredRefs[checkbox] = val ? val : "";
  }
  if (!settings.checkboxStoredRefs[checkbox]) {
    return new Set();
  } else {
    return new Set(settings.checkboxStoredRefs[checkbox].split(",").map(r => convert(r)).filter(a => a >= 0));
  }
}

function getCheckboxState(checkbox, references) {
  var storedRefsSet = getStoredCheckboxRefs(checkbox);
  var currentRefsSet = new Set(references.map(r => r[1]));
  // Get difference of current - stored
  var difference = new Set(currentRefsSet);
  for (ref of storedRefsSet) {
    difference.delete(ref);
  }
  if (difference.size == 0) {
    // All the current refs are stored
    return "checked";
  } else if (difference.size == currentRefsSet.size) {
    // None of the current refs are stored
    return "unchecked";
  } else {
    // Some of the refs are stored
    return "indeterminate";
  }
}

function setBomCheckboxState(checkbox, element, references) {
  var state = getCheckboxState(checkbox, references);
  element.checked = (state == "checked");
  element.indeterminate = (state == "indeterminate");
}

function createCheckboxHandlers(input, checkbox, references, row) {
  var clickHandler = () => {
    refsSet = getStoredCheckboxRefs(checkbox);
    var markWhenChecked = settings.markWhenChecked == checkbox;
    eventArgs = {
      checkbox: checkbox,
      refs: references,
    }
    if (input.checked) {
      // checkbox ticked
      for (var ref of references) {
        refsSet.add(ref[1]);
      }
      if (markWhenChecked) {
        row.classList.add("checked");
        for (var ref of references) {
          markedFootprints.add(ref[1]);
        }
        drawHighlights();
      }
      eventArgs.state = 'checked';
    } else {
      // checkbox unticked
      for (var ref of references) {
        refsSet.delete(ref[1]);
      }
      if (markWhenChecked) {
        row.classList.remove("checked");
        for (var ref of references) {
          markedFootprints.delete(ref[1]);
        }
        drawHighlights();
      }
      eventArgs.state = 'unchecked';
    }
    settings.checkboxStoredRefs[checkbox] = [...refsSet].join(",");
    writeStorage("checkbox_" + checkbox, settings.checkboxStoredRefs[checkbox]);
    updateCheckboxStats(checkbox);
    EventHandler.emitEvent(IBOM_EVENT_TYPES.CHECKBOX_CHANGE_EVENT, eventArgs);
  }

  return [
    (e) => {
      clickHandler();
    },
    (e) => {
      e.preventDefault();
      if (row.onmousemove) row.onmousemove();
    },
    (e) => {
      e.preventDefault();
      input.checked = !input.checked;
      input.indeterminate = false;
      clickHandler();
    }
  ];
}

function clearHighlightedFootprints() {
  if (currentHighlightedRowId) {
    document.getElementById(currentHighlightedRowId).classList.remove("highlighted");
    currentHighlightedRowId = null;
    highlightedFootprints = [];
    highlightedNet = null;
  }
}

function createRowHighlightHandler(rowid, refs, net) {
  return function () {
    if (currentHighlightedRowId) {
      if (currentHighlightedRowId == rowid) {
        return;
      }
      document.getElementById(currentHighlightedRowId).classList.remove("highlighted");
    }
    document.getElementById(rowid).classList.add("highlighted");
    currentHighlightedRowId = rowid;
    highlightedFootprints = refs ? refs.map(r => r[1]) : [];
    highlightedNet = net;
    drawHighlights();
    EventHandler.emitEvent(
      IBOM_EVENT_TYPES.HIGHLIGHT_EVENT, {
      rowid: rowid,
      refs: refs,
      net: net
    });
  }
}

function updateNetColors() {
  writeStorage("netColors", JSON.stringify(settings.netColors));
  redrawIfInitDone();
}

function netColorChangeHandler(net) {
  return (event) => {
    settings.netColors[net] = event.target.value;
    updateNetColors();
  }
}

function netColorRightClick(net) {
  return (event) => {
    if (event.button == 2) {
      event.preventDefault();
      event.stopPropagation();

      var style = getComputedStyle(topmostdiv);
      var defaultNetColor = style.getPropertyValue('--track-color').trim();
      event.target.value = defaultNetColor;
      delete settings.netColors[net];
      updateNetColors();
    }
  }
}

function entryMatches(entry) {
  if (settings.bommode == "netlist") {
    // entry is just a net name
    return entry.toLowerCase().indexOf(filter) >= 0;
  }
  // check refs
  if (!settings.hiddenColumns.includes("References")) {
    for (var ref of entry) {
      if (ref[0].toLowerCase().indexOf(filter) >= 0) {
        return true;
      }
    }
  }
  // check fields
  for (var i in config.fields) {
    var f = config.fields[i];
    if (!settings.hiddenColumns.includes(f)) {
      for (var ref of entry) {
        if (String(pcbdata.bom.fields[ref[1]][i]).toLowerCase().indexOf(filter) >= 0) {
          return true;
        }
      }
    }
  }
  return false;
}

function findRefInEntry(entry) {
  return entry.filter(r => r[0].toLowerCase() == reflookup);
}

function highlightFilter(s) {
  if (!filter) {
    return s;
  }
  var parts = s.toLowerCase().split(filter);
  if (parts.length == 1) {
    return s;
  }
  var r = "";
  var pos = 0;
  for (var i in parts) {
    if (i > 0) {
      r += '<mark class="highlight">' +
        s.substring(pos, pos + filter.length) +
        '</mark>';
      pos += filter.length;
    }
    r += s.substring(pos, pos + parts[i].length);
    pos += parts[i].length;
  }
  return r;
}

function getBomListByLayer(layer) {
  switch (layer) {
    case 'F': return pcbdata.bom.F.slice();
    case 'B': return pcbdata.bom.B.slice();
    case 'FB': return pcbdata.bom.both.slice();
  }
  return [];
}

function getSelectedBomList() {
  if (settings.bommode == "netlist") {
    return pcbdata.nets.slice();
  }
  var out = getBomListByLayer(settings.canvaslayout);

  if (settings.bommode == "ungrouped") {
    // expand bom table
    var expandedTable = [];
    for (var bomentry of out) {
      for (var ref of bomentry) {
        expandedTable.push([ref]);
      }
    }
    return expandedTable;
  }

  return out;
}

function checkboxSetUnsetAllHandler(checkboxname) {
  return function () {
    var checkboxnum = 0;
    while (checkboxnum < settings.checkboxes.length &&
      settings.checkboxes[checkboxnum].toLowerCase() != checkboxname.toLowerCase()) {
      checkboxnum++;
    }
    if (checkboxnum >= settings.checkboxes.length) {
      return;
    }
    var allset = true;
    var checkbox;
    var row;
    for (row of bombody.childNodes) {
      checkbox = row.childNodes[checkboxnum + 1].childNodes[0];
      if (!checkbox.checked || checkbox.indeterminate) {
        allset = false;
        break;
      }
    }
    for (row of bombody.childNodes) {
      checkbox = row.childNodes[checkboxnum + 1].childNodes[0];
      checkbox.checked = !allset;
      checkbox.indeterminate = false;
      checkbox.onchange();
    }
  }
}

function createColumnHeader(name, cls, comparator, is_checkbox = false) {
  var th = document.createElement("TH");
  th.innerHTML = name;
  th.classList.add(cls);
  if (is_checkbox)
    th.setAttribute("col_name", "bom-checkbox");
  else
    th.setAttribute("col_name", name);
  var span = document.createElement("SPAN");
  span.classList.add("sortmark");
  span.classList.add("none");
  th.appendChild(span);
  var spacer = document.createElement("div");
  spacer.className = "column-spacer";
  th.appendChild(spacer);
  spacer.onclick = function () {
    if (currentSortColumn && th !== currentSortColumn) {
      // Currently sorted by another column
      currentSortColumn.childNodes[1].classList.remove(currentSortOrder);
      currentSortColumn.childNodes[1].classList.add("none");
      currentSortColumn = null;
      currentSortOrder = null;
    }
    if (currentSortColumn && th === currentSortColumn) {
      // Already sorted by this column
      if (currentSortOrder == "asc") {
        // Sort by this column, descending order
        bomSortFunction = function (a, b) {
          return -comparator(a, b);
        }
        currentSortColumn.childNodes[1].classList.remove("asc");
        currentSortColumn.childNodes[1].classList.add("desc");
        currentSortOrder = "desc";
      } else {
        // Unsort
        bomSortFunction = null;
        currentSortColumn.childNodes[1].classList.remove("desc");
        currentSortColumn.childNodes[1].classList.add("none");
        currentSortColumn = null;
        currentSortOrder = null;
      }
    } else {
      // Sort by this column, ascending order
      bomSortFunction = comparator;
      currentSortColumn = th;
      currentSortColumn.childNodes[1].classList.remove("none");
      currentSortColumn.childNodes[1].classList.add("asc");
      currentSortOrder = "asc";
    }
    populateBomBody();
  }
  if (is_checkbox) {
    spacer.onclick = fancyDblClickHandler(
      spacer, spacer.onclick, checkboxSetUnsetAllHandler(name));
  }
  return th;
}

function populateBomHeader(placeHolderColumn = null, placeHolderElements = null) {
  while (bomhead.firstChild) {
    bomhead.removeChild(bomhead.firstChild);
  }
  var tr = document.createElement("TR");
  var th = document.createElement("TH");
  th.classList.add("numCol");

  var vismenu = document.createElement("div");
  vismenu.id = "vismenu";
  vismenu.classList.add("menu");

  var visbutton = document.createElement("div");
  visbutton.classList.add("visbtn");
  visbutton.classList.add("hideonprint");

  var viscontent = document.createElement("div");
  viscontent.classList.add("menu-content");
  viscontent.id = "vismenu-content";

  settings.columnOrder.forEach(column => {
    if (typeof column !== "string")
      return;

    // Skip empty columns
    if (column === "checkboxes" && settings.checkboxes.length == 0)
      return;
    else if (column === "Quantity" && settings.bommode == "ungrouped")
      return;

    var label = document.createElement("label");
    label.classList.add("menu-label");

    var input = document.createElement("input");
    input.classList.add("visibility_checkbox");
    input.type = "checkbox";
    input.onchange = function (e) {
      setShowBOMColumn(column, e.target.checked)
    };
    input.checked = !(settings.hiddenColumns.includes(column));

    label.appendChild(input);
    if (column.length > 0)
      label.append(column[0].toUpperCase() + column.slice(1));

    viscontent.appendChild(label);
  });

  viscontent.childNodes[0].classList.add("menu-label-top");

  vismenu.appendChild(visbutton);
  if (settings.bommode != "netlist") {
    vismenu.appendChild(viscontent);
    th.appendChild(vismenu);
  }
  tr.appendChild(th);

  var checkboxCompareClosure = function (checkbox) {
    return (a, b) => {
      var stateA = getCheckboxState(checkbox, a);
      var stateB = getCheckboxState(checkbox, b);
      if (stateA > stateB) return -1;
      if (stateA < stateB) return 1;
      return 0;
    }
  }
  var stringFieldCompareClosure = function (fieldIndex) {
    return (a, b) => {
      var fa = pcbdata.bom.fields[a[0][1]][fieldIndex];
      var fb = pcbdata.bom.fields[b[0][1]][fieldIndex];
      if (fa != fb) return fa > fb ? 1 : -1;
      else return 0;
    }
  }
  var referenceRegex = /(?<prefix>[^0-9]+)(?<number>[0-9]+)/;
  var compareRefs = (a, b) => {
    var ra = referenceRegex.exec(a);
    var rb = referenceRegex.exec(b);
    if (ra === null || rb === null) {
      if (a != b) return a > b ? 1 : -1;
      return 0;
    } else {
      if (ra.groups.prefix != rb.groups.prefix) {
        return ra.groups.prefix > rb.groups.prefix ? 1 : -1;
      }
      if (ra.groups.number != rb.groups.number) {
        return parseInt(ra.groups.number) > parseInt(rb.groups.number) ? 1 : -1;
      }
      return 0;
    }
  }
  if (settings.bommode == "netlist") {
    tr.appendChild(createColumnHeader("Net name", "bom-netname", (a, b) => {
      if (a > b) return -1;
      if (a < b) return 1;
      return 0;
    }));
    tr.appendChild(createColumnHeader("Color", "bom-color", (a, b) => {
      return 0;
    }));
  } else {
    // Filter hidden columns
    var columns = settings.columnOrder.filter(e => !settings.hiddenColumns.includes(e));
    var valueIndex = config.fields.indexOf("Value");
    var footprintIndex = config.fields.indexOf("Footprint");
    columns.forEach((column) => {
      if (column === placeHolderColumn) {
        var n = 1;
        if (column === "checkboxes")
          n = settings.checkboxes.length;
        for (i = 0; i < n; i++) {
          td = placeHolderElements.shift();
          tr.appendChild(td);
        }
        return;
      } else if (column === "checkboxes") {
        for (var checkbox of settings.checkboxes) {
          th = createColumnHeader(
            checkbox, "bom-checkbox", checkboxCompareClosure(checkbox), true);
          tr.appendChild(th);
        }
      } else if (column === "References") {
        tr.appendChild(createColumnHeader("References", "references", (a, b) => {
          var i = 0;
          while (i < a.length && i < b.length) {
            if (a[i][0] != b[i][0]) return compareRefs(a[i][0], b[i][0]);
            i++;
          }
          return a.length - b.length;
        }));
      } else if (column === "Value") {
        tr.appendChild(createColumnHeader("Value", "value", (a, b) => {
          var ra = a[0][1], rb = b[0][1];
          return valueCompare(
            pcbdata.bom.parsedValues[ra], pcbdata.bom.parsedValues[rb],
            pcbdata.bom.fields[ra][valueIndex], pcbdata.bom.fields[rb][valueIndex]);
        }));
        return;
      } else if (column === "Footprint") {
        tr.appendChild(createColumnHeader(
          "Footprint", "footprint", stringFieldCompareClosure(footprintIndex)));
      } else if (column === "Quantity" && settings.bommode == "grouped") {
        tr.appendChild(createColumnHeader("Quantity", "quantity", (a, b) => {
          return a.length - b.length;
        }));
      } else {
        // Other fields
        var i = config.fields.indexOf(column);
        if (i < 0)
          return;
        tr.appendChild(createColumnHeader(
          column, `field${i + 1}`, stringFieldCompareClosure(i)));
      }
    });
  }
  bomhead.appendChild(tr);
}

function populateBomBody(placeholderColumn = null, placeHolderElements = null) {
  const urlRegex = /^(https?:\/\/[^\s\/$.?#][^\s]*|file:\/\/([a-zA-Z]:|\/)[^\x00]+)$/;
  while (bom.firstChild) {
    bom.removeChild(bom.firstChild);
  }
  highlightHandlers = [];
  footprintIndexToHandler = {};
  netsToHandler = {};
  currentHighlightedRowId = null;
  var first = true;
  var style = getComputedStyle(topmostdiv);
  var defaultNetColor = style.getPropertyValue('--track-color').trim();

  bomtable = getSelectedBomList();

  if (bomSortFunction) {
    bomtable = bomtable.sort(bomSortFunction);
  }
  for (var i in bomtable) {
    var bomentry = bomtable[i];
    if (filter && !entryMatches(bomentry)) {
      continue;
    }
    var references = null;
    var netname = null;
    var tr = document.createElement("TR");
    var td = document.createElement("TD");
    var rownum = +i + 1;
    tr.id = "bomrow" + rownum;
    td.textContent = rownum;
    tr.appendChild(td);
    if (settings.bommode == "netlist") {
      netname = bomentry;
      td = document.createElement("TD");
      td.innerHTML = highlightFilter(netname ? netname : "&lt;no net&gt;");
      tr.appendChild(td);
      var color = settings.netColors[netname] || defaultNetColor;
      td = document.createElement("TD");
      var colorBox = document.createElement("INPUT");
      colorBox.type = "color";
      colorBox.value = color;
      colorBox.onchange = netColorChangeHandler(netname);
      colorBox.onmouseup = netColorRightClick(netname);
      colorBox.oncontextmenu = (e) => e.preventDefault();
      td.appendChild(colorBox);
      td.classList.add("color-column");
      tr.appendChild(td);
    } else {
      if (reflookup) {
        references = findRefInEntry(bomentry);
        if (references.length == 0) {
          continue;
        }
      } else {
        references = bomentry;
      }
      // Filter hidden columns
      var columns = settings.columnOrder.filter(e => !settings.hiddenColumns.includes(e));
      columns.forEach((column) => {
        if (column === placeholderColumn) {
          var n = 1;
          if (column === "checkboxes")
            n = settings.checkboxes.length;
          for (i = 0; i < n; i++) {
            td = placeHolderElements.shift();
            tr.appendChild(td);
          }
          return;
        } else if (column === "checkboxes") {
          for (var checkbox of settings.checkboxes) {
            if (checkbox) {
              td = document.createElement("TD");
              var input = document.createElement("input");
              input.type = "checkbox";
              [input.onchange, td.ontouchstart, td.ontouchend] = createCheckboxHandlers(input, checkbox, references, tr);
              setBomCheckboxState(checkbox, input, references);
              if (input.checked && settings.markWhenChecked == checkbox) {
                tr.classList.add("checked");
              }
              td.appendChild(input);
              tr.appendChild(td);
            }
          }
        } else if (column === "References") {
          td = document.createElement("TD");
          td.innerHTML = highlightFilter(references.map(r => r[0]).join(", "));
          tr.appendChild(td);
        } else if (column === "Quantity" && settings.bommode == "grouped") {
          // Quantity
          td = document.createElement("TD");
          td.textContent = references.length;
          tr.appendChild(td);
        } else {
          // All the other fields
          var field_index = config.fields.indexOf(column)
          if (field_index < 0)
            return;
          var valueSet = new Set();
          references.map(r => r[1]).forEach((id) => valueSet.add(pcbdata.bom.fields[id][field_index]));
          td = document.createElement("TD");
          var output = new Array();
          for (let item of valueSet) {
            const visible = highlightFilter(String(item));
            if (typeof item === 'string' && item.match(urlRegex)) {
              output.push(`<a href="${item}" target="_blank">${visible}</a>`);
            } else {
              output.push(visible);
            }
          }
          td.innerHTML = output.join(", ");
          tr.appendChild(td);
        }
      });
    }
    bom.appendChild(tr);
    var handler = createRowHighlightHandler(tr.id, references, netname);
    if (settings.highlightRowOnClick) {
      tr.onmousedown = handler;
    } else {
      tr.onmousemove = handler;
    }
    highlightHandlers.push({
      id: tr.id,
      handler: handler,
    });
    if (references !== null) {
      for (var refIndex of references.map(r => r[1])) {
        footprintIndexToHandler[refIndex] = handler;
      }
    }
    if (netname !== null) {
      netsToHandler[netname] = handler;
    }
    if ((filter || reflookup) && first) {
      handler();
      first = false;
    }
  }
  EventHandler.emitEvent(
    IBOM_EVENT_TYPES.BOM_BODY_CHANGE_EVENT, {
    filter: filter,
    reflookup: reflookup,
    checkboxes: settings.checkboxes,
    bommode: settings.bommode,
  });
}

function highlightPreviousRow() {
  if (!currentHighlightedRowId) {
    highlightHandlers[highlightHandlers.length - 1].handler();
  } else {
    if (highlightHandlers.length > 1 &&
      highlightHandlers[0].id == currentHighlightedRowId) {
      highlightHandlers[highlightHandlers.length - 1].handler();
    } else {
      for (var i = 0; i < highlightHandlers.length - 1; i++) {
        if (highlightHandlers[i + 1].id == currentHighlightedRowId) {
          highlightHandlers[i].handler();
          break;
        }
      }
    }
  }
  smoothScrollToRow(currentHighlightedRowId);
}

function highlightNextRow() {
  if (!currentHighlightedRowId) {
    highlightHandlers[0].handler();
  } else {
    if (highlightHandlers.length > 1 &&
      highlightHandlers[highlightHandlers.length - 1].id == currentHighlightedRowId) {
      highlightHandlers[0].handler();
    } else {
      for (var i = 1; i < highlightHandlers.length; i++) {
        if (highlightHandlers[i - 1].id == currentHighlightedRowId) {
          highlightHandlers[i].handler();
          break;
        }
      }
    }
  }
  smoothScrollToRow(currentHighlightedRowId);
}

function populateBomTable() {
  populateBomHeader();
  populateBomBody();
  setBomHandlers();
  resizableGrid(bomhead);
}

function footprintsClicked(footprintIndexes) {
  var lastClickedIndex = footprintIndexes.indexOf(lastClicked);
  for (var i = 1; i <= footprintIndexes.length; i++) {
    var refIndex = footprintIndexes[(lastClickedIndex + i) % footprintIndexes.length];
    if (refIndex in footprintIndexToHandler) {
      lastClicked = refIndex;
      footprintIndexToHandler[refIndex]();
      smoothScrollToRow(currentHighlightedRowId);
      break;
    }
  }
}

function netClicked(net) {
  if (net in netsToHandler) {
    netsToHandler[net]();
    smoothScrollToRow(currentHighlightedRowId);
  } else {
    clearHighlightedFootprints();
    highlightedNet = net;
    drawHighlights();
  }
}

function updateFilter(input) {
  filter = input.toLowerCase();
  populateBomTable();
}

function updateRefLookup(input) {
  reflookup = input.toLowerCase();
  populateBomTable();
}

function changeCanvasLayout(layout) {
  document.getElementById("fl-btn").classList.remove("depressed");
  document.getElementById("fb-btn").classList.remove("depressed");
  document.getElementById("bl-btn").classList.remove("depressed");
  switch (layout) {
    case 'F':
      document.getElementById("fl-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.collapse(1);
      }
      break;
    case 'B':
      document.getElementById("bl-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.collapse(0);
      }
      break;
    default:
      document.getElementById("fb-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.setSizes([50, 50]);
      }
  }
  settings.canvaslayout = layout;
  writeStorage("canvaslayout", layout);
  resizeAll();
  changeBomMode(settings.bommode);
}

function populateMetadata() {
  document.getElementById("title").innerHTML = pcbdata.metadata.title;
  document.getElementById("revision").innerHTML = "Rev: " + pcbdata.metadata.revision;
  document.getElementById("company").innerHTML = pcbdata.metadata.company;
  document.getElementById("filedate").innerHTML = pcbdata.metadata.date;
  if (pcbdata.metadata.title != "") {
    document.title = pcbdata.metadata.title + " BOM";
  }
  // Calculate board stats
  var fp_f = 0,
    fp_b = 0,
    pads_f = 0,
    pads_b = 0,
    pads_th = 0;
  for (var i = 0; i < pcbdata.footprints.length; i++) {
    if (pcbdata.bom.skipped.includes(i)) continue;
    var mod = pcbdata.footprints[i];
    if (mod.layer == "F") {
      fp_f++;
    } else {
      fp_b++;
    }
    for (var pad of mod.pads) {
      if (pad.type == "th") {
        pads_th++;
      } else {
        if (pad.layers.includes("F")) {
          pads_f++;
        }
        if (pad.layers.includes("B")) {
          pads_b++;
        }
      }
    }
  }
  document.getElementById("stats-components-front").innerHTML = fp_f;
  document.getElementById("stats-components-back").innerHTML = fp_b;
  document.getElementById("stats-components-total").innerHTML = fp_f + fp_b;
  document.getElementById("stats-groups-front").innerHTML = pcbdata.bom.F.length;
  document.getElementById("stats-groups-back").innerHTML = pcbdata.bom.B.length;
  document.getElementById("stats-groups-total").innerHTML = pcbdata.bom.both.length;
  document.getElementById("stats-smd-pads-front").innerHTML = pads_f;
  document.getElementById("stats-smd-pads-back").innerHTML = pads_b;
  document.getElementById("stats-smd-pads-total").innerHTML = pads_f + pads_b;
  document.getElementById("stats-th-pads").innerHTML = pads_th;
  // Update version string
  document.getElementById("github-link").innerHTML = "InteractiveHtmlBom&nbsp;" +
    /^v\d+\.\d+/.exec(pcbdata.ibom_version)[0];
}

function changeBomLayout(layout) {
  document.getElementById("bom-btn").classList.remove("depressed");
  document.getElementById("lr-btn").classList.remove("depressed");
  document.getElementById("tb-btn").classList.remove("depressed");
  switch (layout) {
    case 'bom-only':
      document.getElementById("bom-btn").classList.add("depressed");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      document.getElementById("frontcanvas").style.display = "none";
      document.getElementById("backcanvas").style.display = "none";
      document.getElementById("topmostdiv").style.height = "";
      document.getElementById("topmostdiv").style.display = "block";
      break;
    case 'top-bottom':
      document.getElementById("tb-btn").classList.add("depressed");
      document.getElementById("frontcanvas").style.display = "";
      document.getElementById("backcanvas").style.display = "";
      document.getElementById("topmostdiv").style.height = "100%";
      document.getElementById("topmostdiv").style.display = "flex";
      document.getElementById("bomdiv").classList.remove("split-horizontal");
      document.getElementById("canvasdiv").classList.remove("split-horizontal");
      document.getElementById("frontcanvas").classList.add("split-horizontal");
      document.getElementById("backcanvas").classList.add("split-horizontal");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      bomsplit = Split(['#bomdiv', '#canvasdiv'], {
        sizes: [50, 50],
        onDragEnd: resizeAll,
        direction: "vertical",
        gutterSize: 5
      });
      canvassplit = Split(['#frontcanvas', '#backcanvas'], {
        sizes: [50, 50],
        gutterSize: 5,
        onDragEnd: resizeAll
      });
      break;
    case 'left-right':
      document.getElementById("lr-btn").classList.add("depressed");
      document.getElementById("frontcanvas").style.display = "";
      document.getElementById("backcanvas").style.display = "";
      document.getElementById("topmostdiv").style.height = "100%";
      document.getElementById("topmostdiv").style.display = "flex";
      document.getElementById("bomdiv").classList.add("split-horizontal");
      document.getElementById("canvasdiv").classList.add("split-horizontal");
      document.getElementById("frontcanvas").classList.remove("split-horizontal");
      document.getElementById("backcanvas").classList.remove("split-horizontal");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      bomsplit = Split(['#bomdiv', '#canvasdiv'], {
        sizes: [50, 50],
        onDragEnd: resizeAll,
        gutterSize: 5
      });
      canvassplit = Split(['#frontcanvas', '#backcanvas'], {
        sizes: [50, 50],
        gutterSize: 5,
        direction: "vertical",
        onDragEnd: resizeAll
      });
  }
  settings.bomlayout = layout;
  writeStorage("bomlayout", layout);
  changeCanvasLayout(settings.canvaslayout);
}

function changeBomMode(mode) {
  document.getElementById("bom-grouped-btn").classList.remove("depressed");
  document.getElementById("bom-ungrouped-btn").classList.remove("depressed");
  document.getElementById("bom-netlist-btn").classList.remove("depressed");
  var chkbxs = document.getElementsByClassName("visibility_checkbox");

  switch (mode) {
    case 'grouped':
      document.getElementById("bom-grouped-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = false;
      }
      break;
    case 'ungrouped':
      document.getElementById("bom-ungrouped-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = false;
      }
      break;
    case 'netlist':
      document.getElementById("bom-netlist-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = true;
      }
  }

  writeStorage("bommode", mode);
  if (mode != settings.bommode) {
    settings.bommode = mode;
    bomSortFunction = null;
    currentSortColumn = null;
    currentSortOrder = null;
    clearHighlightedFootprints();
  }
  populateBomTable();
}

function focusFilterField() {
  focusInputField(document.getElementById("filter"));
}

function focusRefLookupField() {
  focusInputField(document.getElementById("reflookup"));
}

function toggleBomCheckbox(bomrowid, checkboxnum) {
  if (!bomrowid || checkboxnum > settings.checkboxes.length) {
    return;
  }
  var bomrow = document.getElementById(bomrowid);
  var childNum = checkboxnum + settings.columnOrder.indexOf("checkboxes");
  var checkbox = bomrow.childNodes[childNum].childNodes[0];
  checkbox.checked = !checkbox.checked;
  checkbox.indeterminate = false;
  checkbox.onchange();
}

function checkBomCheckbox(bomrowid, checkboxname) {
  var checkboxnum = 0;
  while (checkboxnum < settings.checkboxes.length &&
    settings.checkboxes[checkboxnum].toLowerCase() != checkboxname.toLowerCase()) {
    checkboxnum++;
  }
  if (!bomrowid || checkboxnum >= settings.checkboxes.length) {
    return;
  }
  var bomrow = document.getElementById(bomrowid);
  var childNum = checkboxnum + 1 + settings.columnOrder.indexOf("checkboxes");
  var checkbox = bomrow.childNodes[childNum].childNodes[0];
  checkbox.checked = true;
  checkbox.indeterminate = false;
  checkbox.onchange();
}

function setBomCheckboxes(value) {
  writeStorage("bomCheckboxes", value);
  settings.checkboxes = value.split(",").map((e) => e.trim()).filter((e) => e);
  prepCheckboxes();
  populateMarkWhenCheckedOptions();
  setMarkWhenChecked(settings.markWhenChecked);
}

function setMarkWhenChecked(value) {
  writeStorage("markWhenChecked", value);
  settings.markWhenChecked = value;
  markedFootprints.clear();
  for (var ref of (value ? getStoredCheckboxRefs(value) : [])) {
    markedFootprints.add(ref);
  }
  populateBomTable();
  drawHighlights();
}

function prepCheckboxes() {
  var table = document.getElementById("checkbox-stats");
  while (table.childElementCount > 1) {
    table.removeChild(table.lastChild);
  }
  if (settings.checkboxes.length) {
    table.style.display = "";
  } else {
    table.style.display = "none";
  }
  for (var checkbox of settings.checkboxes) {
    var tr = document.createElement("TR");
    var td = document.createElement("TD");
    td.innerHTML = checkbox;
    tr.appendChild(td);
    td = document.createElement("TD");
    td.id = "checkbox-stats-" + checkbox;
    var progressbar = document.createElement("div");
    progressbar.classList.add("bar");
    td.appendChild(progressbar);
    var text = document.createElement("div");
    text.classList.add("text");
    td.appendChild(text);
    tr.appendChild(td);
    table.appendChild(tr);
    updateCheckboxStats(checkbox);
  }
}

function populateMarkWhenCheckedOptions() {
  var container = document.getElementById("markWhenCheckedContainer");

  if (settings.checkboxes.length == 0) {
    container.parentElement.style.display = "none";
    return;
  }

  container.innerHTML = '';
  container.parentElement.style.display = "inline-block";

  function createOption(name, displayName) {
    var id = "markWhenChecked-" + name;

    var div = document.createElement("div");
    div.classList.add("radio-container");

    var input = document.createElement("input");
    input.type = "radio";
    input.name = "markWhenChecked";
    input.value = name;
    input.id = id;
    input.onchange = () => setMarkWhenChecked(name);
    div.appendChild(input);

    // Preserve the selected element when the checkboxes change
    if (name == settings.markWhenChecked) {
      input.checked = true;
    }

    var label = document.createElement("label");
    label.innerHTML = displayName;
    label.htmlFor = id;
    div.appendChild(label);

    container.appendChild(div);
  }
  createOption("", "None");
  for (var checkbox of settings.checkboxes) {
    createOption(checkbox, checkbox);
  }
}

function updateCheckboxStats(checkbox) {
  var checked = getStoredCheckboxRefs(checkbox).size;
  var total = pcbdata.footprints.length - pcbdata.bom.skipped.length;
  var percent = checked * 100.0 / total;
  var td = document.getElementById("checkbox-stats-" + checkbox);
  td.firstChild.style.width = percent + "%";
  td.lastChild.innerHTML = checked + "/" + total + " (" + Math.round(percent) + "%)";
}

function constrain(number, min, max) {
  return Math.min(Math.max(parseInt(number), min), max);
}

document.onkeydown = function (e) {
  switch (e.key) {
    case "n":
      if (document.activeElement.type == "text") {
        return;
      }
      if (currentHighlightedRowId !== null) {
        checkBomCheckbox(currentHighlightedRowId, "placed");
        highlightNextRow();
        e.preventDefault();
      }
      break;
    case "ArrowUp":
      highlightPreviousRow();
      e.preventDefault();
      break;
    case "ArrowDown":
      highlightNextRow();
      e.preventDefault();
      break;
    case "ArrowLeft":
    case "ArrowRight":
      if (document.activeElement.type != "text") {
        e.preventDefault();
        let boardRotationElement = document.getElementById("boardRotation")
        settings.boardRotation = parseInt(boardRotationElement.value);  // degrees / 5
        if (e.key == "ArrowLeft") {
          settings.boardRotation += 3;  // 15 degrees
        }
        else {
          settings.boardRotation -= 3;
        }
        settings.boardRotation = constrain(settings.boardRotation, boardRotationElement.min, boardRotationElement.max);
        boardRotationElement.value = settings.boardRotation
        setBoardRotation(settings.boardRotation);
      }
      break;
    default:
      break;
  }
  if (e.altKey) {
    switch (e.key) {
      case "f":
        focusFilterField();
        e.preventDefault();
        break;
      case "r":
        focusRefLookupField();
        e.preventDefault();
        break;
      case "z":
        changeBomLayout("bom-only");
        e.preventDefault();
        break;
      case "x":
        changeBomLayout("left-right");
        e.preventDefault();
        break;
      case "c":
        changeBomLayout("top-bottom");
        e.preventDefault();
        break;
      case "v":
        changeCanvasLayout("F");
        e.preventDefault();
        break;
      case "b":
        changeCanvasLayout("FB");
        e.preventDefault();
        break;
      case "n":
        changeCanvasLayout("B");
        e.preventDefault();
        break;
      default:
        break;
    }
    if (e.key >= '1' && e.key <= '9') {
      toggleBomCheckbox(currentHighlightedRowId, parseInt(e.key));
      e.preventDefault();
    }
  }
}

function hideNetlistButton() {
  document.getElementById("bom-ungrouped-btn").classList.remove("middle-button");
  document.getElementById("bom-ungrouped-btn").classList.add("right-most-button");
  document.getElementById("bom-netlist-btn").style.display = "none";
}

function topToggle() {
  var top = document.getElementById("top");
  var toptoggle = document.getElementById("toptoggle");
  if (top.style.display === "none") {
    top.style.display = "flex";
    toptoggle.classList.remove("flipped");
  } else {
    top.style.display = "none";
    toptoggle.classList.add("flipped");
  }
}

window.onload = function (e) {
  initRender();
  initStorage();
  initDefaults();
  initUtils();
  cleanGutters();
  populateMetadata();
  dbgdiv = document.getElementById("dbg");
  bom = document.getElementById("bombody");
  bomhead = document.getElementById("bomhead");
  filter = "";
  reflookup = "";
  if (!("nets" in pcbdata)) {
    hideNetlistButton();
  }
  initDone = true;
  setBomCheckboxes(document.getElementById("bomCheckboxes").value);
  // Triggers render
  changeBomLayout(settings.bomlayout);

  // Users may leave fullscreen without touching the checkbox. Uncheck.
  document.addEventListener('fullscreenchange', () => {
    if (!document.fullscreenElement)
      document.getElementById('fullscreenCheckbox').checked = false;
  });
}

window.onresize = resizeAll;
window.matchMedia("print").addListener(resizeAll);

///////////////////////////////////////////////

///////////////////////////////////////////////

///////////////////////////////////////////////
  </script>
</head>

<body>

<div id="topmostdiv" class="topmostdiv">
  <div id="top">
    <div id="fileinfodiv">
      <table class="fileinfo">
        <tbody>
          <tr>
            <td id="title" class="title" style="width: 70%">
              Title
            </td>
            <td id="revision" class="title" style="width: 30%">
              Revision
            </td>
          </tr>
          <tr>
            <td id="company">
              Company
            </td>
            <td id="filedate">
              Date
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div id="bomcontrols">
      <div class="hideonprint menu">
        <button class="menubtn"></button>
        <div class="menu-content">
          <label class="menu-label menu-label-top" style="width: calc(50% - 18px)">
            <input id="darkmodeCheckbox" type="checkbox" onchange="setDarkMode(this.checked)">
            Dark mode
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label menu-label-top" style="width: calc(50% - 17px); border-left: 0;">
            <input id="fullscreenCheckbox" type="checkbox" onchange="setFullscreen(this.checked)">
            Full Screen
          </label>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="fabricationCheckbox" type="checkbox" checked onchange="fabricationVisible(this.checked)">
            Fab layer
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="silkscreenCheckbox" type="checkbox" checked onchange="silkscreenVisible(this.checked)">
            Silkscreen
          </label>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="referencesCheckbox" type="checkbox" checked onchange="referencesVisible(this.checked)">
            References
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="valuesCheckbox" type="checkbox" checked onchange="valuesVisible(this.checked)">
            Values
          </label>
          <div id="tracksAndZonesCheckboxes">
            <label class="menu-label" style="width: calc(50% - 18px)">
              <input id="tracksCheckbox" type="checkbox" checked onchange="tracksVisible(this.checked)">
              Tracks
            </label><!-- This comment eats space! All of it!
            --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
              <input id="zonesCheckbox" type="checkbox" checked onchange="zonesVisible(this.checked)">
              Zones
            </label>
          </div>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="padsCheckbox" type="checkbox" checked onchange="padsVisible(this.checked)">
            Pads
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="dnpOutlineCheckbox" type="checkbox" checked onchange="dnpOutline(this.checked)">
            DNP outlined
          </label>
          <label class="menu-label">
            <input id="highlightRowOnClickCheckbox" type="checkbox" checked onchange="setHighlightRowOnClick(this.checked)">
            Highlight row on click
          </label>
          <label class="menu-label">
            <input id="dragCheckbox" type="checkbox" checked onchange="setRedrawOnDrag(this.checked)">
            Continuous redraw on drag
          </label>
          <label class="menu-label">
            Highlight first pin
            <form id="highlightpin1">
              <div class="flexbox">
                <label>
                  <input type="radio" name="highlightpin1" value="none" onchange="setHighlightPin1('none')">
                  None
                </label>
                <label>
                  <input type="radio" name="highlightpin1" value="all" onchange="setHighlightPin1('all')">
                  All
                </label>
                <label>
                  <input type="radio" name="highlightpin1" value="selected" onchange="setHighlightPin1('selected')">
                  Selected
                </label>
              </div>
            </form>
          </label>
          <label class="menu-label">
            <span>Board rotation</span>
            <span style="float: right"><span id="rotationDegree">0</span>&#176;</span>
            <input id="boardRotation" type="range" min="-36" max="36" value="0" class="slider" oninput="setBoardRotation(this.value)">
          </label>
          <label class="menu-label">
            <input id="offsetBackRotationCheckbox" type="checkbox" onchange="setOffsetBackRotation(this.checked)">
            Offset back rotation
          </label>
          <label class="menu-label">
            <div style="margin-left: 5px">Bom checkboxes</div>
            <input id="bomCheckboxes" class="menu-textbox" type=text
                   oninput="setBomCheckboxes(this.value)">
          </label>
          <label class="menu-label">
            <div style="margin-left: 5px">Mark when checked</div>
            <div id="markWhenCheckedContainer"></div>
          </label>
          <label class="menu-label">
            <span class="shameless-plug">
              <span>Created using</span>
              <a id="github-link" target="blank" href="https://github.com/openscopeproject/InteractiveHtmlBom">InteractiveHtmlBom</a>
              <a target="blank" title="Mouse and keyboard help" href="https://github.com/openscopeproject/InteractiveHtmlBom/wiki/Usage#bom-page-mouse-actions" style="text-decoration: none;"><label class="help-link">?</label></a>
            </span>
          </label>
        </div>
      </div>
      <div class="button-container hideonprint">
        <button id="fl-btn" class="left-most-button" onclick="changeCanvasLayout('F')"
                title="Front only">F
        </button>
        <button id="fb-btn" class="middle-button" onclick="changeCanvasLayout('FB')"
                title="Front and Back">FB
        </button>
        <button id="bl-btn" class="right-most-button" onclick="changeCanvasLayout('B')"
                title="Back only">B
        </button>
      </div>
      <div class="button-container hideonprint">
        <button id="bom-btn" class="left-most-button" onclick="changeBomLayout('bom-only')"
                title="BOM only"></button>
        <button id="lr-btn" class="middle-button" onclick="changeBomLayout('left-right')"
                title="BOM left, drawings right"></button>
        <button id="tb-btn" class="right-most-button" onclick="changeBomLayout('top-bottom')"
                title="BOM top, drawings bot"></button>
      </div>
      <div class="button-container hideonprint">
        <button id="bom-grouped-btn" class="left-most-button" onclick="changeBomMode('grouped')"
                title="Grouped BOM"></button>
        <button id="bom-ungrouped-btn" class="middle-button" onclick="changeBomMode('ungrouped')"
                title="Ungrouped BOM"></button>
        <button id="bom-netlist-btn" class="right-most-button" onclick="changeBomMode('netlist')"
                title="Netlist"></button>
      </div>
      <div class="hideonprint menu">
        <button class="statsbtn"></button>
        <div class="menu-content">
          <table class="stats">
            <tbody>
              <tr>
                <td width="40%">Board stats</td>
                <td>Front</td>
                <td>Back</td>
                <td>Total</td>
              </tr>
              <tr>
                <td>Components</td>
                <td id="stats-components-front">~</td>
                <td id="stats-components-back">~</td>
                <td id="stats-components-total">~</td>
              </tr>
              <tr>
                <td>Groups</td>
                <td id="stats-groups-front">~</td>
                <td id="stats-groups-back">~</td>
                <td id="stats-groups-total">~</td>
              </tr>
              <tr>
                <td>SMD pads</td>
                <td id="stats-smd-pads-front">~</td>
                <td id="stats-smd-pads-back">~</td>
                <td id="stats-smd-pads-total">~</td>
              </tr>
              <tr>
                <td>TH pads</td>
                <td colspan=3 id="stats-th-pads">~</td>
              </tr>
            </tbody>
          </table>
          <table class="stats">
            <col width="40%"/><col />
            <tbody id="checkbox-stats">
              <tr>
                <td colspan=2 style="border-top: 0">Checkboxes</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <div class="hideonprint menu">
        <button class="iobtn"></button>
        <div class="menu-content">
          <div class="menu-label menu-label-top">
            <div style="margin-left: 5px;">Save board image</div>
            <div class="flexbox">
              <input id="render-save-width" class="menu-textbox" type="text" value="1000" placeholder="Width"
                  style="flex-grow: 1; width: 50px;" oninput="validateSaveImgDimension(this)">
              <span>X</span>
              <input id="render-save-height" class="menu-textbox" type="text" value="1000" placeholder="Height"
                  style="flex-grow: 1; width: 50px;" oninput="validateSaveImgDimension(this)">
            </div>
            <label>
              <input id="render-save-transparent" type="checkbox">
              Transparent background
            </label>
            <div class="flexbox">
              <button class="savebtn" onclick="saveImage('F')">Front</button>
              <button class="savebtn" onclick="saveImage('B')">Back</button>
            </div>
          </div>
          <div class="menu-label">
            <span style="margin-left: 5px;">Config and checkbox state</span>
            <div class="flexbox">
              <button class="savebtn" onclick="saveSettings()">Export</button>
              <button class="savebtn" onclick="loadSettings()">Import</button>
              <button class="savebtn" onclick="resetSettings()">Reset</button>
            </div>
          </div>
          <div class="menu-label">
            <span style="margin-left: 5px;">Save bom table as</span>
            <div class="flexbox">
              <button class="savebtn" onclick="saveBomTable('csv')">csv</button>
              <button class="savebtn" onclick="saveBomTable('txt')">txt</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="topdivider">
    <div class="hideonprint">
      <div id="toptoggle" onclick="topToggle()">︽</div>
    </div>
  </div>
  <div id="bot" class="split" style="flex: 1 1">
    <div id="bomdiv" class="split split-horizontal">
      <div style="width: 100%">
        <input id="reflookup" class="textbox searchbox reflookup hideonprint" type="text" placeholder="Ref lookup"
               oninput="updateRefLookup(this.value)">
        <input id="filter" class="textbox searchbox filter hideonprint" type="text" placeholder="Filter"
               oninput="updateFilter(this.value)">
        <div class="button-container hideonprint" style="float: left; margin: 0;">
          <button id="copy" title="Copy bom table to clipboard"
               onclick="saveBomTable('clipboard')"></button>
        </div>
      </div>
      <div id="dbg"></div>
      <table class="bom" id="bomtable">
        <thead id="bomhead">
        </thead>
        <tbody id="bombody">
        </tbody>
      </table>
    </div>
    <div id="canvasdiv" class="split split-horizontal">
      <div id="frontcanvas" class="split" touch-action="none" style="overflow: hidden">
        <div style="position: relative; width: 100%; height: 100%;">
          <canvas id="F_bg" style="position: absolute; left: 0; top: 0; z-index: 0;"></canvas>
          <canvas id="F_fab" style="position: absolute; left: 0; top: 0; z-index: 1;"></canvas>
          <canvas id="F_slk" style="position: absolute; left: 0; top: 0; z-index: 2;"></canvas>
          <canvas id="F_hl" style="position: absolute; left: 0; top: 0; z-index: 3;"></canvas>
        </div>
      </div>
      <div id="backcanvas" class="split" touch-action="none" style="overflow: hidden">
        <div style="position: relative; width: 100%; height: 100%;">
          <canvas id="B_bg" style="position: absolute; left: 0; top: 0; z-index: 0;"></canvas>
          <canvas id="B_fab" style="position: absolute; left: 0; top: 0; z-index: 1;"></canvas>
          <canvas id="B_slk" style="position: absolute; left: 0; top: 0; z-index: 2;"></canvas>
          <canvas id="B_hl" style="position: absolute; left: 0; top: 0; z-index: 3;"></canvas>
        </div>
      </div>
    </div>
  </div>
</div>

</body>

</html>
