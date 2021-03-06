# REST API med Postman
Først skal vi repetere hvordan vi bruker et API med Postman som klient. Vi skal bruke nettsiden APIet på nettsiden gorest.co.in (samme som sist).

Gå inn på:
```postman.com```
og logg inn med brukeren din.

## Sette opp collection i Postman

For å holde ting ryddig i postman skal vi opprette en **collection** som skal inneholde alle **requestene** vi skriver.

For å opprette en collection i Postman, trykk på "+" tegnet til høyre for "Collections" knappen:

![Skjermdump: Hvordan opprette en collection](./img/postman_new_collection.png)


Den nye collectionen kan du kalle hva du vil, f.eks. "gorest.co.in", som er nettsiden vi skal bruke.

## Repetisjon: Request med GET

Nå skal vi skrive vår første request.

Den enkleste requesten er GET, som vi bruker når vi skal hente informarsjon fra serveren vi snakker med. Vi kan begynne med å hente brukeren for gorest-siden.

Trykk for å legge til en ny request rett under tittelen på den ny kolleksjonen:

![Skjermdump: Hvordan legge til en request](./img/postman_add_request.png)

Da får vi opp vinduet for å redigere den nye requesten.

Øverst er navnet på requesten. Det er bare for vår egen den for å holde styr på ting. Vi kan kalle denne "Hent alle brukere".

Nedenfor skriver vi URLen for requesten. Vi skal hente ut brukerene i gorest-siden, urlen blir derfor:

```https://gorest.co.in/public/v1/users```


Med alle verdiene satt kan vi trykke på Send-knappen helt til høyre:

![Skjermdump: Hvordan sende en request](./img/postman_send_request.png)

Requesten blir da sendt til serveren på den gitte URLen, og postman viser oss svaret, en **Response**, vi får tilbake i JSON-format:

![Skjermdump: Respons fra en request](./img/postman_response.png)

### Oppgave: Hente alle innlegg

Opprett en GET request i samme kolleksjon som henter alle innleggene fra endepunktet:

```https://gorest.co.in/public/v1/posts```

For å opprette en ny request er det enkleste å duplisere en eksisterende ved å trykke på "···"-menyen og velge "Duplicate" eller ved å bruke snarveien "⌘D"

Ta et skjermbilde av den ferdige requesten med både Request og Response synlig.

## Request med autorisering

Vi skal nå gå videre til requester hvor vi kan opprette brukere og innlegg, men da trenger vi å autorisere oss. Vi skal bruke en **token** som vi sender med sammen med requesten vår for å bevise at vi har tilgang til å opprette ting i nettsiden.

I timen vil det bli lagt ut en token i teams. Hvis du jobber med dette på egenhånd kan du gå inn på https://gorest.co.in/access-token for å lage en egen token.

Fordi alle kallene mot gorest-siden kan bruke samme token, skal vi legge til tokenet på collection, ikke på enkelt request, trykk derfor direkte på collection-navnet.

I kolleksjonen velger vi "Autorization"-tabben. I "Type" menyen velger du "Bearer Token", og lim inn tokenet inn i "Token"-feltet, som vist på bildet:

![Skjermdump: Hvordan sette opp authorization i en collection](./img/postman_auth.png)

Nå vil tokenet automatisk brukes i alle requests i kolleksjonen.

## Repetisjon: Request med POST

Vi skal nå opprette en ny bruker på serveren. For å gjøre dette må vi gjøre en request av typen POST.

For å opprette en ny request er det enkleste å duplisere en eksisterende ved å trykke på "···"-menyen og velge "Duplicate" eller ved å bruke snarveien "⌘D"

![Skjermdump: Hvordan duplisere en request i postman](./img/postman_duplicate.png)

Vi endrer navnet på requesten til "Opprett bruker", limer inn samme URL som da vi hentet brukere, og trykker på "GET" for å velge metoden "POST" i menyen. Requesten blir da slik:

![Skjermdump: Hvordan duplisere en request i postman](./img/postman_post_request.png)

Hvis vi trykker "Send" får vi se at serveren mottar requesten vår, godtar autoriseringen, men ikke godtar requesten. Dette er fordi requesten mangler informasjon om den nye brukeren vi skal opprette. Vi kjenner igjen feltene `email`, `name`, `gender` og `status` fra svaret på GET-requesten vi sendte tidligere.

Denne informasjonen skal vi legge i **body** i requesten. Vi bruker JSON-format, samme format som i svaret vi fikk. Velg "Body"-taben, velg "raw" og trykk på "Text" for å få opp meny hvor du kan velge "JSON". Det trenger vi for at postman skal sende riktig, og vi får også syntax-hjelp i body-vinduet.

![Skjermdump: Hvordan velge JSON som body i postman](./img/postman_empty_body.png)

I tekstboksen rett under URL (hvor det er `{}` i eksempel-bildet) fyller vi inn JSON med informasjon om brukeren, f.eks:

```javascript
{
    "email": "test@email.com",
    "name": "Andreas Test",
    "gender": "male",
    "status": "active"
}
```

Vi har navn på feltet til venstre og verdien til høyre, skilt av et kolon ":". Mellom hvert par av navn og verdi har vi et komma.

Når vi trykker "Send" får vi svar med den nye brukeren som er opprettet:

![Skjermdump: Svaret fra en POST-request i postman](./img/postman_post_response.png)

### Oppgave: Opprett et innlegg

Opprett en POST request i samme kolleksjon som oppretter ett innlegg med endepunktet:

```https://gorest.co.in/public/v1/posts```

Du kan se hvilke felter som trenger å være med i svaret på GET-requesten, eller i feilmeldingen om du sender en tom POST-request. 

Ta et skjermbilde av den ferdige requesten med Request og Response i synlig.

## Oppsummering

Vi har nå repetert hvordan vi bruker Postman til å gjøre REST API Requester mot en server.

En Request består av fire deler:

1. en **URL** som sier hvilken ressurs det er vi skal gjøre noe med. I eksemplene over gjør vi noe users, så dermed er urlen https://gorest.co.in/public/v1/users.

2. en **metode** som sier hva det er vi skal gjøre med ressursen. Vi bruker metoden "GET" når vi henter ut brukere. Vi bruker metoden "POST" når vi oppretter en ny.

3. **Headere**. Disse har postman fylt ut for oss, så vi kommer tilbake til dem senere.

4. Requesten kan også ha en **Body**, hvis vi skal laste opp informasjon. 


Svaret vi får tilbake på en Request er en **Response**. En response har også headere og kan ha en body, men har ikke en URL eller en metode.

Body i Request og Response kan være i ulike format. Vi har sett formatet JSON, som er veldig vanlig. Når du åpner en vanlig webside blir det gjort en GET-request mot URLen i nettleseren. Nettsiden du får se er i Responsen sin body. Formatet er da HTML.

## Innlevering

Du skal levere inn i de to skjermbildene i teams.