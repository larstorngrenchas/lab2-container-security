# Lab 2 Container Security

A school project with Docker, Trivy, Kubernetes

# Vad lärde du dig om container-säkerhet?
Det jag lärde mig om container-säkerhet, är att ju mer man bantar bort från en image, desto säkrare blir den container man sedan skapar från sin image. Säkrast blir det med en distroless image, eftersom det då inte finns några paket och inga systemkommandon att använda sig av för den som försöker hacka systemet. En annan säkerhetsåtgärd är att skapa en användare som enbart har behörighet att köra en specifik app inuti containern, som då körs som non-root.

# Varför är SBOM viktigt?
SBOM talar om vilka komponenter som finns i den app som finns i en container. Vilket är viktigt både ur felsökningsperspektiv, spårbarhet i mjukvaruutveckling och för säkerheten.

# Hur förändrar policy-enforcement (Gatekeeper) hur man jobbar med Kubernetes?
Man tvingar utvecklare att vara noggranna, och kontrollera sin kod innan man kör deployment, eftersom det annars blir så att en pod nekas vid skapandet. Det gör även att säkerhetsarbetet blir mer automatiserat och policydrivet. All mjukvara som skapas måste gå igenom policykontrollen för att bli godkänd.
