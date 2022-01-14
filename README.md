# basics-yaml
Aprendendo sintaxe e feature do yaml

## YAML
E uma linguagem superset para o JSON e largamente usado em dev ops </br>
Configurações de pipe lines,aws,git cli

##
## Feature
- Como qualquer linguagem ele possui amplamente suporte aos tipos escalares, “string”, number,float,null
- Strings são particularmente representados de n maneiras com aspas duplas,sem aspas
- Também e possível de forma implícita determinar o tipo escalar com !!
- Se converter para JSON vai perceber que ao determinar float para 16, vai ser convertido para 16.0

``` yaml


YAML is superset of json: !!bool true 
Pluto is a planet: !!bool false
positive-float: !!float 16
key with null value: !!null null
sampleNumString: !!str 8.14


```

##

- Yaml possui recurso de reaproveitamento de código, com a palavra reservada &
- No exemplo abaixo todos  valores determinados apos & foram reaproveitados
- Para yaml entender oque esta abaixo e objeto ou array você utiliza o - apos a palavra
- No exemplo abaixo - weekday e uma palavra-chave dependendo do comportamento abaixo vai ser um array ou objeto
- Para ser array precisam estar duas casas a frente e com -, para ser objetos apenas duas casas já e o suficiente

``` yaml


definitions:
  days:
    - weekday: &working 
        makeup: 6:00
        actives:
          - workout
          - meetings
          - sleep
        sleeptime: 10:00 pm 
    - weekend:
        makeup: any hours
        actives: don't have, i am free

schedules:
  days:
    weekdays:
      - Monday: *working 
      - Tuesday: *working
      - Thursday: *working
      - Friday: *working

# array com obojetos
# objeto inicia em - name

profession: 
   - name: Ricardo kenji
    id: 3
    department: development
  - name: Rafael Kioji
    id: 4
    department: engineer


```

##

- Outro recurso interessante que você consegue subscrever valores que reaproveitou usando <<:
- Tambem e  possível trabalhar com multi arquivos, para este recuso basta terminar o início com --- e o final com ...
- E útil quando em poucas linhas deseja ambientes diferentes,detalhe se converter para JSON não ira refletir poque  não tem suporte a multi arquivos

``` yaml
definitions:
  days:
    - weekday: &working
        makeup: 6:00
        actives:
          - workout
          - meetings
          - sleep
        sleeptime: 10:00 pm
    - weekend:
        makeup: any hours
        actives: don't have, i am free

schedules:
  days:
    weekdays:
      - Monday: *working #serao inseridos aqui
      - Tuesday: *working
      - Thursday: *working
      - Friday:
        <<: *working #precisa ser assim apara ele entender a mudanca
        sleeptime: 12:00 pm #peguei o valor e fiz um override antes era 10 agora vai ser 12



```














