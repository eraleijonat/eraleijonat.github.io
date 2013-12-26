---
title:    join
template: index.jade
---

## Jäsenhakemus

Olet hakemassa jäsenyyttä **Helsingin Erä-Leijonat ry**:hyn ja samalla **Suomen Partiolaiset ry**:hyn. Jos täytät lomaketta lapsesi puolesta, ole hyvä ja täytä myös huoltajan tiedot.

Jäsenen on maksettava Suomen Partiolaisten jäsenmaksu ja lisäksi mahdollinen lippukunnan jäsenmaksu, jos sellaista kerätään nykyisellä toimintakaudella. Suomen Partiolaiset ry lähettää laskun postissa.

<form>
  
  <h3>Hakijan tiedot</h3>

  <label for="firstNames">Etunimet</label>
  <input id="firstNames" type="text" placeholder="Etunimet" />

  <label for="lastName">Sukunimi</label>
  <input id="lastName" type="text" placeholder="Sukunimi" />

  <label for="address">Osoite</label>
  <textarea id="address" rows="4" placeholder="Postiosoite"></textarea>

  <label for="birth-date">Syntymäaika</label>
  <select id="birth-date">
    <option value="1">1.</option>
    <option value="2">2.</option>
    <option value="3">3.</option>
    <option value="4">4.</option>
    <option value="5">5.</option>
    <option value="6">6.</option>
    <option value="7">7.</option>
    <option value="8">8.</option>
    <option value="9">9.</option>
    <option value="10">10.</option>
    <option value="11">11.</option>
    <option value="12">12.</option>
    <option value="13">13.</option>
    <option value="14">14.</option>
    <option value="15">15.</option>
    <option value="16">16.</option>
    <option value="17">17.</option>
    <option value="18">18.</option>
    <option value="19">19.</option>
    <option value="20">20.</option>
    <option value="21">21.</option>
    <option value="22">22.</option>
    <option value="23">23.</option>
    <option value="24">24.</option>
    <option value="25">25.</option>
    <option value="26">26.</option>
    <option value="27">27.</option>
    <option value="28">28.</option>
    <option value="29">29.</option>
    <option value="30">30.</option>
    <option value="31">31.</option>
  </select>
  <select id="birth-month">
    <option value="1">tammikuuta</option>
    <option value="2">helmikuuta</option>
    <option value="3">maaliskuuta</option>
    <option value="4">huhtikuuta</option>
    <option value="5">toukokuuta</option>
    <option value="6">kesäkuuta</option>
    <option value="7">heinäkuuta</option>
    <option value="8">elokuuta</option>
    <option value="9">syyskuuta</option>
    <option value="10">lokakuuta</option>
    <option value="11">marraskuuta</option>
    <option value="12">joulukuuta</option>
  </select>
  <input id="birth-year" placeholder="Vuosi" />

  <label for="phone">Puhelinnumero</label>
  <input id="phone" type="text" placeholder="Puhelinnumero" />

  <label for="email">Sähköpostiosoite</label>
  <input id="email" type="text" placeholder="Sähköposti" />

  <h3>Huoltajan tiedot</h3>

  <p>Täytettävä, jos hakija on alle 18-vuotias.</p>

  <label for="huoltaja-name">Huoltajan nimi</label>
  <input id="huoltaja-name" type="text" placeholder="Huoltajan nimi" />
  
  <label for="huoltaja-phone">Huoltajan puhelinnumero</label>
  <input id="huoltaja-phone" type="text" placeholder="Huoltajan puhelinnumero" />

  <label for="huoltaja-email">Huoltajan sähköpostiosoite</label>
  <input id="huoltaja-email" type="text" placeholder="Huoltajan sähköposti" />

  <h3>Lisätiedot</h3>

  <textarea id="details" placeholder="Vapaa lisätietokenttä. Onko kysyttävää, haluatko meidän ottavan yhteyttä, tms.?"></textarea>

  <button type="button" id="submit">Lähetä hakemus</button>
</form>

<p id="submit-result"></p>

### Rekisteriseloste

Syöttämäsi tiedot tallennetaan Suomen Partiolaisten sähköiseen Polku-jäsenrekisteriin. Henkilötietolain 10 §:n mukainen [rekisteriseloste on saatavilla SP:n sivuilla](http://toiminta.partio.fi/sites/partio.fi/files/polku_rekisteriseloste.pdf).

<script type="text/javascript">

  var $button = document.getElementById("submit");
  var $result = document.getElementById("submit-result");

  /* ei mitään jQuerya :) */

  var value = function(id) {
    return document.getElementById(id).value;
  };

  var showResult = function(id) {
    $result.style.display = "block";
  };

  var send = function() {

    var url = "http://eraleijonat-emailer.herokuapp.com/new-member";
    
    var params = {
      "firstNames":     value("firstNames"),
      "lastName":       value("lastName"),
      "address":        value("address"),
      "dob":            value("birth-date") + "." + value("birth-month") + "." + value("birth-year"),
      "phone":          value("phone"),
      "email":          value("email"),
      "huoltaja-name":  value("huoltaja-name"),
      "huoltaja-phone": value("huoltaja-phone"),
      "huoltaja-email": value("huoltaja-email"),
      "details":        value("details")
    };

  var fail = function(result) {
    $result.innerHTML = result.fail;
    showResult();
  }

  var succeed = function(result) {
    $result.innerHTML = result.success;
    showResult();
    $button.disabled = "true";
  }

    var xhr = new XMLHttpRequest();
    xhr.open("POST", url, true);
    xhr.setRequestHeader("Content-type", "application/json; charset=utf-8");
    
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        var result = JSON.parse(xhr.responseText);

        if (xhr.status === 200 && result.success) succeed(result);
        else fail(result);
      }
    }
    
    xhr.send(JSON.stringify(params));
  }

  document.getElementById("submit").onclick = function() {
    $result.innerHTML = "Hakemusta lähetetään...";
    send();
  }
</script>