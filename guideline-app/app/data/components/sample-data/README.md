## Live-eksempler - How-to

Alle live-komponentene m/tilhørende kodeeksempler i Guideline-appen er basert på 
JS-objektene som eksporteres ut fra hver enkelt fil under ```sample-data/```, og alt skal fungere
out-of-the-box gitt at JS-objektet som eksporteres ut fra ```sample-data/_[komponentnavn].js``` 
og videre ut fra ```sample-data/index.js```, blir satt opp riktig.
 
 
### Dataformatet

Datatformatet for å få live-eksemplene til å funke, består i hovedsak av to konsepter;
typer (types) og modifikatorer (modifiers). 

En egen type legger alltid grunnlag for en egen komponent. F.eks. er ```AlertStripeSuksess```,
```AlertStripeInfo``` og ```AlertStripeAdvarsel```, alle tre forskjellige typer. Men her er det også
lagt inn støtte for å spesifisere 1 <= attributter for å indikere typen.   
 
Modifikatorer legger grunnlag for en egen komponent, eller 1 <= attributter, avhengig av om 
typen man modifiserer kan ha en eller flere modifikatorer. Til eksempel har Alertstripe-komponentene
kun en modifikator, som er ```solid```, og gir grunnlag for komponentene ```AlertStripeSuksessSolid```
og ```AlertStripeInfoSolid```. For tilfeller med flere aktive modifikatorer på en gang, f.eks. knapp-komponentene, som har
tre modifikatorer, ```mini```, ```spinner``` og ```disabled```, setter man istedet dette opp
som attributter for komponenttypene ```Knapp```, ```Hovedknapp``` og ```Fareknapp```. 

For eksempler, se på de ulike ```_[komponentnavn].js``` filene som allerede ligger i ```sample-data/```. 

### Fullstendig datastruktur:

```
{
    types: [
        {
            component,
            attrs: {
                key: value
            },
            children,
            label,
            _default,
            modifiers: [
                { value, component },
                ...
            ]
       }
    ],
    modifiers: [
        { value, label, _default },
        ...
    ],
    multipleChoiceModifiers: [
        { value, label },
        ...
    ]
}

```

#### Type
| Attributt                | Type     | Beskrivelse                                                                      | Required |
| ------------------------ | -------- | ---------------------------------------------------------------------------------| -------- |
| component                | function | React-komponenten som skal brukes for typen                                      | true     |
| attrs                    | object   | (k,v)-par av attributter som skal settes på komponenten                          | false    |
| children                 | function | React-komponent som skal vises som child i eksemplet                             | false    |
| label                    | string   | Label til radio-knapp for typen i live-eksemplet                                 | true     |
| _default                 | boolean  | Radio-knapp for typen er default huket av                                        | false    |
| modifiers                | array    | Modifier-value (string mappet til modifiers på rot) med komponent som skal vises | false    |
| multipleChoiceModifiers  | array    | Multiple-choice modifikatorer for typen (=checkbox)                              | false    |

#### Modifiers
| Attributt                | Type     | Beskrivelse                                                           | Required |
| ------------------------ | -------- | --------------------------------------------------------------------- | -------- |
| value                    | string   | Navn på modifier (mappes til type.modifiers hvis gjeldende for typen) | true     |
| label                    | string   | Label til radio-knapp for modifikatoren i live-eksemplet              | true     |
| _default                 | boolean  | Radio.knapp for modifikatoren er default huket av                     | false    |


#### MultipleChoiceModifiers
| Attributt                | Type     | Beskrivelse                                                 | Required |
| ------------------------ | -------- | ----------------------------------------------------------- | -------- |
| value                    | string   | Navn på modifier (blir til til value=true på komponenten)   | true     |
| label                    | string   | Label til checkbox-knapp for modifikatoren i live-eksemplet | true     |
