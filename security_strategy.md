# Min säkerhetsstrategi

## Kräva etiketter på alla pods
Vi får förbättrad säkerhet genom att ”NetworkPolicies” använder labels för att styra vilken podd som får prata med vilken. Tvingande labels förhindrar att poddar hamnar utanför säkerhetsregler.
Med standardiserade labels blir även felsökningen smidigare då loggar och mätvärden (metrics) enkelt kan aggregeras och filtreras i verktyg som Prometheus eller Grafana.
Genom att kräva etiketter (”labels”) blir det också lättare att filtrera, gruppera och hantera resurser med kubectl. Det underlättar dessutom för att tilldela resursanvändning (CPU/minne) till specifika team eller applikationer för kostnadsuppföljning och internfakturering.
Labels kan också användas för schemaläggning och automatiserad drift, exempelvis för att styra pod-affinitet/anti-affinitet, vilket gör att man kan tvinga poddar att köras på specifika noder (t.ex. med dyrare GPU) eller sprida dem över tillgänglighetszoner.

## Sätta både krav på att ange resursbehov, men också ett maxtak (MaxResourceLimits)
Det ger flexibilitet genom att vi kan ha en ”hård” begränsning för produktion och en ”mildare” för test-miljön genom att bara ändra i Constraint-filen. Det ger ett standardiserat arbetssätt som gör att vi slipper skriva ny kod varje gång kraven ändras. Det blir säkrare genom att det förhindrar ”Resource Exhaustion” (att en buggig pod äter upp alla resurser på noden).

## Kräva att containers körs som non-root
Genom att kräva ett User ID (tillsammans med runAsNonRoot) säkerställer vi att containern inte bara är non-root, utan faktiskt körs som en specifik användare som inte är 0 (root).
Vi förhindrar därigenom ”Privilege Escalation”. Om en container körs som root och blir hackad, är det mycket enklare för angriparen att ta över hela noden (hosten). Det ger förutsägbarhet i klustret om alla appar följer samma regler.

## Mutation i kombination med constraint
Samarbetet med utvecklarna blir bättre, för de behöver inte kunna alla säkerhetsinställningar utantill, klustret fixar deras YAML-filer automatiskt. Vi får en standardiserad säkerhetsnivå som garanterar att allt som körs i klustret följer våra regler genom att blockera farliga val eller missar, även om någon glömmer att skriva det i sin deployment. Vi undviker att få massor av felmeddelanden med ”Denied” i våra CI/CD-pipelines.
