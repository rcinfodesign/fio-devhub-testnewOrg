---
title: Test4
description: Test4
---

<select id="integrator-dropdown" name="integrators">
</select>

<script>
  var integrator = "Edge"

  let dropdown = $('#integrator-dropdown');
  dropdown.empty();
  dropdown.append('<option selected="true" disabled>Choose Integrator</option>');
  dropdown.prop('selectedIndex', 0);

  $.getJSON("integrations.json", function (data) {
    $.each(data, function (key, entry) {
      dropdown.append($('<option></option>').attr('value', key).text(key));
    })
  });

  $("#integrator-dropdown").change(function() {
    var selected = $(this).find(':selected');
    $.getJSON("integrations.json", function(result) {
      $.each(result, function(i, idata) {
        if (i == selected.val()) {
          $.each(idata.features, function(feature, avail) {
            // First clear it, then fill it if true
            $("#" + feature).attr({"src": ""});
            if (avail) {$("#" + feature).attr({"src": "/assets/img/completed.png"});};
          });
        }
      });
    });
  });
</script>


<table>
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>FIO Token</td>
      <td>Create FIO Wallet</td>
      <td> <img id="token-createwallet" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Check FIO Balance</td>
      <td> <img id="token-checkbalance" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Transfer FIO</td>
      <td> <img id="token-transferfio" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Transaction history</td>
      <td> <img id="token-txnhistory" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Import FIO Private Key</td>
      <td> <img id="token-importkey" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Import mnemonic phrase</td>
      <td> <img id="token-importphrase" src=""> </td>
    </tr>
    <tr>
      <td>FIO Address</td>
      <td>Register FIO Address on wallet domain (api or link to reg site)</td>
      <td> <img id="address-register" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Renew FIO address</td>
      <td> <img id="address-renew" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Display registered FIO Addresses</td>
      <td> <img id="address-show" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Register FIO Address on custom domain</td>
      <td> <img id="address-customdomain" src=""> </td>
    </tr>
    <tr>
      <td>FIO Domains</td>
      <td>Register FIO Domain (api or link to reg site)</td>
      <td> <img id="domain-renew" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Renew FIO Domain</td>
      <td> <img id="createwallet" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Display registered FIO Domains</td>
      <td> <img id="domain-show" src=""> </td>
    </tr>
    <tr>
      <td>FIO Send</td>
      <td>Send crypto using FIO Address</td>
      <td> <img id="send-send" src=""> </td>
    </tr>
    <tr>
      <td>FIO Receive</td>
      <td>Receive crypto using FIO Address (via direct send)</td>
      <td> <img id="receive-receive" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Map FIO Address to other blockchain public addreses</td>
      <td> <img id="receive-map" src=""> </td>
    </tr>
    <tr>
      <td>FIO Requests</td>
      <td>Submitting new FIO Request</td>
      <td> <img id="request-submit" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Rejecting a FIO Request</td>
      <td> <img id="request-reject" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>List pending FIO Requests</td>
      <td> <img id="request-pending" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>List sent FIO Requests</td>
      <td> <img id="request-sent" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Add memo to the FIO Request</td>
      <td> <img id="request-requestmemo" src=""> </td>
    </tr>
    <tr>
      <td>FIO Data</td>
      <td>Record OBT on Send and other FIO Transactions</td>
      <td> <img id="data-recordobt" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Retrieve and displaying OBT data</td>
      <td> <img id="data-displayobt" src=""> </td>
    </tr>
    <tr>
      <td> </td>
      <td>Add a memo when creating an OBT Record</td>
      <td> <img id="data-memo" src=""> </td>
    </tr>
  </tbody>
</table>
