# APL Easings

A collection of cubic-bezier easings for the Alexa Platform Language (APL), based on Robert Penner's Easing Functions

### Adding to APL Project

You can import all Easings as an [APL package](https://developer.amazon.com/pt-BR/docs/alexa/alexa-presentation-language/apl-package.html), or simply add the ones you'll need within the [Resources](https://developer.amazon.com/pt-BR/docs/alexa/alexa-presentation-language/apl-resources.html) block of your APL doc.


### Importing as a Package

Copy the file [apl-easings.json](https://github.com/stephenscaff/APL-Easings/apl-easings.json) to some publicly stored location, and import into APL as a package:

```
{
    "type": "APL",
    "version": "1.1",
    "import": [
        {
            "name": "apl-easings",
            "version": "https:/someplace.com/<path>/apl-easings.json"
        }
    ]
    ....
}
```

### Adding what you need to Resources
APL Resources are named entities accessible through data-binding and value resolution. Basically, they are stored variables that can be referenced from an APL layout or component. You can simply copy the easings you want:


```
{
  "type": "APL",
  "version": "1.1",
  "resources": [
    {
      "description": "Easing Functions as cubic-bezier",
      "values": {
          "easeInSine": "cubic-bezier(0.47, 0, 0.745, 0.715)",
          "easeOutSine": "cubic-bezier(0.39, 0.575, 0.565, 1)",
          "easeInOutSine": "cubic-bezier(0.445, 0.05, 0.55, 0.95)",
          "easeInQuad": "cubic-bezier(0.55, 0.085, 0.68, 0.53)"
          ....
      }
    }
  ]
}
```


### Using

APL Resources are accessed using `@resourceName`.

So, you would reference easeInSine, like `@easeInSine`.

For these easings, you will be applying them to the `easing` property of the `AnimateItem` command.

*Like This*
```

"onMount": [
  {
    "type": "AnimateItem",
    'componentId': "someComponent",
    "duration": "300",
    "easing": "@easeInQuint",
    "value": [
      {
        "property": "transform",
        "from": [
            {
                "translateX": "100%"
            }
        ],
        "to": [
            {
                "translateX": 0
            }
        ]
      }
    ]
  }
]
```

*Or Perhaps as a saved command*


```
"fadeInLeft": {
  "parameters": [
      "duration",
      "delay",
      "easing",
      "amount"
  ],
  "commands": [
      {
          "type": "AnimateItem",
          "duration": "${duration || 400}",
          "delay": "${delay || 0}",
          "easing": "${easing || @easeInExpo}",
          "value": [
              {
                  "property": "opacity",
                  "to": 1
              },
              {
                  "property": "transform",
                  "from": [
                      {
                          "translateX": "${amount || 10}"
                      }
                  ],
                  "to": [
                      {
                          "translateX": 0
                      }
                  ]
              }
          ]
      }
  ]
}
```
