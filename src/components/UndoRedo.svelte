<style>
  div {
    cursor: pointer;
    font-size: 0.7rem;
    height: 100%;
    justify-items: center;
    display: grid;
    grid-gap: 2px;
    padding-right: 1rem;
    grid-template-areas:
      "undo redo"
      "undoLabel redoLabel";
  }
  label {
    cursor: pointer;
  }
  #undo {
    align-self: end;
    grid-area: undo;
  }
  #redo {
    align-self: end;
    grid-area: redo;
  }
  #undoLabel {
    color:#bbb;
    grid-area: undoLabel;
  }
  #redoLabel {
    color:#bbb;
    grid-area: redoLabel;
  }
</style>

<div>
  <svg id="undo" style="width:1rem;height:1rem" viewBox="0 0 24 24">
    <path
      fill="#bbb"
      d="M12.5,8C9.85,8 7.45,9 5.6,10.6L2,7V16H11L7.38,12.38C8.77,11.22
      10.54,10.5 12.5,10.5C16.04,10.5 19.05,12.81
      20.1,16L22.47,15.22C21.08,11.03 17.15,8 12.5,8Z" />
  </svg>
  <label id="undoLabel">undo</label>
  <svg id="redo" style="width:1rem;height:1rem" viewBox="0 0 24 24">
    <path
      fill="#bbb"
      d="M18.4,10.6C16.55,9 14.15,8 11.5,8C6.85,8 2.92,11.03
      1.54,15.22L3.9,16C4.95,12.81 7.95,10.5 11.5,10.5C13.45,10.5 15.23,11.22
      16.62,12.38L13,16H22V7L18.4,10.6Z" />
  </svg>
  <label id="redoLabel">redo</label>
</div>
