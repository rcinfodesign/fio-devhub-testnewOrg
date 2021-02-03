---
title: Test
description: Test
---


<div>
    {% assign integrators = site.data.integrations.integrators %}
    <label for="integratorlist">Select:</label>
    <select name="integratorlist" onchange="javascript:location.href = this.value;">
        {% for integrator in integrators %}
            <option value="{{integrator.name}}" >{{ integrator.name }}</option>
        {% endfor %}
    </select>
</div>

{% assign testname = "edge" %}

{% include checklist.html name=testname %}


