# Lab 2 Container Security

A school project with Docker, Trivy, Kubernetes

## Vad som genomförts
Jag har skapat två olika docker images. Den ena med medvetet bristande säkerhetstänkande (vulnerable image), den andra med säkerhet i åtanke (hardened image). Sedan har jag scannat respektive image med Trivy, och sparat resultatet både som en skärmdump, och som rapporter i text-format (rapport för den första imagen, före hardening, och sedan rapport för den andra imagen, efter hardening). Därefter genererade jag med CyclonDX en SBOM (Software Bill Of Materials) för att få fram en lista av de olika komponenter som ingår i appen jag skapar. Viktigt både för spårbarhet och säkerhet. Slutligen använde jag Gatekeeper för att kunna se befintliga policies och eventuella violations i mitt namespace. Jag genomförde också ett test som jämförde en ”bad pod” med en ”hardened pod”. Jag lade sedan in några policies i mitt projekt.

## Verktyg som har använts
Verktygen jag har använt är terminalen, Docker, Trivy, VS Code, CyclonDX, Gatekeeper.

## Vad lärde du dig om container-säkerhet?
Det jag lärde mig om container-säkerhet, är att ju mer man bantar bort från en image (gör den ”slim”), desto säkrare blir den container man sedan skapar från sin image. Säkrast blir det med en distroless image, eftersom det då inte finns några paket och inga systemkommandon att använda sig av för den som försöker hacka systemet. Ytterligare säkerhetsåtgärder är att skapa ett ReadOnly-filsystem, och en användare som enbart har behörighet att köra en specifik app inuti containern, som då körs som non-root.

## Varför är SBOM viktigt?
SBOM talar om vilka komponenter som finns i den app som finns i en container. Vilket är viktigt både ur felsökningsperspektiv, spårbarhet i mjukvaruutveckling och för säkerheten.

## Hur förändrar policy-enforcement (Gatekeeper) hur man jobbar med Kubernetes?
Man tvingar utvecklare att vara noggranna, och kontrollera sin kod innan man kör deployment, eftersom det annars blir så att en pod nekas vid skapandet. Det gör även att säkerhetsarbetet blir mer automatiserat och policydrivet. All mjukvara som skapas måste gå igenom policykontrollen för att bli godkänd.

## Skärmdumpar
![Trivy scanning before hardening](screenshots/trivy-before.jpg)
![Trivy scanning efter hardening](screenshots/trivy-after.jpg)
![Gatekeeper deny](screenshots/gatekeeper-deny.jpg)
![Gatekeeper pass](screenshots/gatekeeper-pass.jpg)

## Cosigned docker hardened image
![Cosigning hardened docker image](screenshots/cosigned_docker_image_dockerhub.jpg)