---
title: Test3
description: Test3
---

<button>Get External Content</button>

<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").load("demo_test.txt", function(responseTxt, statusTxt, xhr){
      if(statusTxt == "success")
        alert("External content loaded successfully!");
      if(statusTxt == "error")
        alert("Error: " + xhr.status + ": " + xhr.statusText);
    });
  });
});
</script>

<div id="div1"><h2>Let jQuery AJAX Change This Text</h2></div>

