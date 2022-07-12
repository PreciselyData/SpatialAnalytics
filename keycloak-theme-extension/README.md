# keycloak-theme-extension

This is a repo for custom themes in precisely branding for SWP Keycloak.

---

## Getting Started
Git clone this repository and cd into to the project directory

### Prerequisites

Prerequisite for viewing the themes is a local Keycloak installation. 
1. You can follow this [tutorial](https://www.keycloak.org/docs/latest/getting_started/).
2. Start the local Keycloak server
```bash
cd <path-to-keycloak>
bin/standalone.bat
```
This will start the keycloak server on `http://localhost:8080` 

## Develop theme

### Initialize theme

1. From inside this repository, make a copy of the `theme/precisely` folder. Name the new folder an appropriate name. This will be your new theme.
2. Customize this folder to match your needs. Follow the [official documentation](https://www.keycloak.org/docs/latest/server_development/#_themes).

> Note: This repository is shared by all themes. Do not make changes to other themes.

### Package theme

1. Edit the `META-INF/keycloak-themes.json` file to add your theme. Themes not added to this file will not be discovered by Keycloak. More info [here](https://www.keycloak.org/docs/latest/server_development/#deploying-themes)
```json
{
    "themes": [                        # This is a list of objects. One object per theme. Do not edit other objects.
        {
            "name": "precisely", # must be same name as your theme folder.
            "types": [                 # You can add only the types you edited and leave the rest. You usually want to leave all 5.
                "login",
                "email",
                "welcome",
                "admin",
                "account"
            ]
        } 
    ]
}
```

2. The theme is packaged as a jar file. 
```bash
gradlew clean build
```
This last command will create a `keycloak-theme-extension-x.x.jar` file in `build\libs` folder where `x.x` is the version set earlier.

### Deploy theme in keycloak Distribution powered by Quarkus (v18.0.0)
1. You will need to copy the packaged theme into the deployments folder of Keycloak and it will be loaded automatically. 

Drag and drop or run the following command:

```bash
cp keycloak-custom-theme/target/theme-x.x.x.jar <path-to-local-keycloak>/providers/
```
2. Wait a minute and restart the browser. Your theme shall show up under the drop down in the Keycloak realm settings.

