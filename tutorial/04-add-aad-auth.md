---
ms.openlocfilehash: 3e4d7f11c89947da29873c85ab2808279c94265a
ms.sourcegitcommit: 189f87d879c57b11992e7bc75580b4c69e014122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "43612064"
---
<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD. Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph. En este paso, integrará la [biblioteca de autenticación de Microsoft (MSAL) para Java](https://github.com/AzureAD/microsoft-authentication-library-for-java) en la aplicación.

1. Cree un nuevo directorio denominado **graphtutorial** en el directorio **./src/Main/Resources**

1. Cree un nuevo archivo en el directorio **./src/Main/Resources/graphtutorial** denominado **OAuth. Properties**y agregue el siguiente texto en ese archivo.

    :::code language="ini" source="../demo/graphtutorial/src/main/resources/graphtutorial/oAuth.properties.example":::

    Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación que creó en Azure portal.

    > [!IMPORTANT]
    > Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **OAuth. Properties** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.

1. Abra **app. Java** y agregue las siguientes `import` instrucciones.

    ```java
    import java.io.IOException;
    import java.util.Properties;
    ```

1. Agregue el siguiente código justo antes de `Scanner input = new Scanner(System.in);` la línea para cargar el archivo **OAuth. Properties** .

    :::code language="java" source="../demo/graphtutorial/src/main/java/graphtutorial/App.java" id="LoadSettingsSnippet":::

## <a name="implement-sign-in"></a>Implementar el inicio de sesión

1. Cree un nuevo archivo en el directorio **./graphtutorial/src/Main/Java/graphtutorial** denominado **Authentication. Java** y agregue el código siguiente.

    :::code language="java" source="../demo/graphtutorial/src/main/java/graphtutorial/Authentication.java" id="AuthenticationSnippet":::

1. En **app. Java**, agregue el siguiente código justo antes de `Scanner input = new Scanner(System.in);` la línea para obtener un token de acceso.

    ```java
    // Get an access token
    Authentication.initialize(appId);
    final String accessToken = Authentication.getUserAccessToken(appScopes);
    ```

1. Agregue la siguiente línea después del `// Display access token` comentario.

    ```java
    System.out.println("Access token: " + accessToken);
    ```

1. Ejecute la aplicación. La aplicación muestra una dirección URL y un código de dispositivo.

    ```Shell
    Java Graph Tutorial

    To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code F7CG945YZ to authenticate.
    ```

1. Abra un explorador y vaya a la dirección URL que se muestra. Escriba el código proporcionado e inicie sesión. Una vez finalizado, vuelva a la aplicación y elija el **1. Muestra** la opción de token de acceso para mostrar el token de acceso.
