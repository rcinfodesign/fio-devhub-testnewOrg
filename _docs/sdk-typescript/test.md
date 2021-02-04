---
title: Test
description: Test
---


<div>
    {% assign integrators = site.data.integrations.integrators %}
    <label for="integratorlist">Select:</label>
    <select name="ilist" id="ilist">
        {% for integrator in integrators %}
            <option value="newvalue" >{{ integrator.name }}</option>
        {% endfor %}
    </select>
</div>

<div id="mydiv">
adfadsfadsf
    {% assign testname = 'edge' %}
    {% include checklist.html name=testname %}
</div>

    

<script>
$(function() {
  $('#ilist').change(function() {
    
    $('#mydiv').html(this.value);

  });


});
</script>

