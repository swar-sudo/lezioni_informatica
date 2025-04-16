# Guida alla Creazione di un Web Service SOAP con Java in Eclipse

Creare un web service SOAP utilizzando Java ed Eclipse è un'ottima introduzione al mondo dei servizi web. Questa guida vi accompagnerà passo dopo passo nella creazione di un semplice servizio SOAP, dalla configurazione dell'ambiente di sviluppo fino alla realizzazione e test del servizio.

## Prerequisiti:

Prima di iniziare, assicuratevi di avere:
- Eclipse IDE installato (preferibilmente Eclipse IDE for Enterprise Java and Web Developers)
- JDK (Java Development Kit) installato, versione 8 o superiore
- Apache Tomcat configurato in Eclipse (versione 8 o superiore)
- Connessione internet per scaricare eventuali librerie necessarie

## 1. Configurazione dell'Ambiente di Sviluppo

### 1.1 Installazione e Configurazione di Eclipse

1. Aprite Eclipse e selezionate un workspace per il vostro progetto.
2. Verificate che Eclipse abbia la prospettiva Java EE attiva (in alto a destra potete selezionare la prospettiva).
3. Assicuratevi che Tomcat sia configurato correttamente:
   - Andate su Window > Preferences > Server > Runtime Environments
   - Se non trovate Tomcat nella lista, cliccate su "Add" e selezionate la versione di Tomcat che avete installato
   - Specificare il percorso della directory di installazione di Tomcat

## 2. Creazione del Progetto Web

### 2.1 Creare un nuovo Progetto Dynamic Web Project

1. File > New > Dynamic Web Project
2. Assegnate un nome al progetto (es. "SoapWebServiceDemo")
3. Selezionate come Target Runtime il server Apache Tomcat configurato in precedenza
4. Impostate la versione del Dynamic Web Module a 3.0 o superiore
5. Selezionate la configurazione di default
6. Importante: assicuratevi che sia selezionata l'opzione "Generate web.xml deployment descriptor"
7. Cliccate su "Finish" per creare il progetto

## 3. Creazione delle Classi per il Web Service

### 3.1 Creare il Package per il Web Service

1. Cliccate con il tasto destro sulla cartella "src" del progetto
2. Selezionate New > Package
3. Assegnate un nome al package (es. "it.scuola.webservice")
4. Cliccate su "Finish"

### 3.2 Creare la Classe di Servizio

1. Cliccate con il tasto destro sul package appena creato
2. Selezionate New > Class
3. Assegnate un nome alla classe (es. "CalcolatriceService")
4. Cliccate su "Finish"
5. Implementate la classe con alcune operazioni semplici:

```java
package it.scuola.webservice;

import javax.jws.WebService;
import javax.jws.WebMethod;
import javax.jws.WebParam;

@WebService(serviceName="CalcolatriceService")
public class CalcolatriceService {
    
    @WebMethod(operationName="somma")
    public int somma(@WebParam(name="a") int a, @WebParam(name="b") int b) {
        return a + b;
    }
    
    @WebMethod(operationName="sottrazione")
    public int sottrazione(@WebParam(name="a") int a, @WebParam(name="b") int b) {
        return a - b;
    }
    
    @WebMethod(operationName="moltiplicazione")
    public int moltiplicazione(@WebParam(name="a") int a, @WebParam(name="b") int b) {
        return a * b;
    }
    
    @WebMethod(operationName="divisione")
    public double divisione(@WebParam(name="a") int a, @WebParam(name="b") int b) {
        if (b == 0) {
            throw new ArithmeticException("Divisione per zero non consentita");
        }
        return (double) a / b;
    }
}
```

In questo codice:
- `@WebService` indica che questa classe rappresenta un servizio web
- `@WebMethod` identifica i metodi che saranno esposti come operazioni del servizio web
- `@WebParam` permette di specificare il nome dei parametri nel WSDL generato

## 4. Configurazione del Web Service

### 4.1 Creare la Classe di Pubblicazione

1. Cliccate con il tasto destro sul package
2. Selezionate New > Class
3. Assegnate un nome alla classe (es. "CalcolatricePublisher")
4. Cliccate su "Finish"
5. Implementate la classe di pubblicazione:

```java
package it.scuola.webservice;

import javax.xml.ws.Endpoint;

public class CalcolatricePublisher {
    public static void main(String[] args) {
        // Indirizzo dove verrà pubblicato il servizio
        String address = "http://localhost:8080/SoapWebServiceDemo/calcolatrice";
        
        // Creazione dell'endpoint con la classe di implementazione del servizio
        Endpoint.publish(address, new CalcolatriceService());
        
        System.out.println("Servizio pubblicato all'indirizzo: " + address);
        System.out.println("WSDL disponibile all'indirizzo: " + address + "?wsdl");
    }
}
```

### 4.2 Configurare il file web.xml

Modificate il file web.xml nella cartella WEB-INF con il seguente contenuto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://java.sun.com/xml/ns/javaee"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
    id="WebApp_ID" version="3.0">
    
    <display-name>SoapWebServiceDemo</display-name>
    
    <listener>
        <listener-class>com.sun.xml.ws.transport.http.servlet.WSServletContextListener</listener-class>
    </listener>
    
    <servlet>
        <servlet-name>CalcolatriceService</servlet-name>
        <servlet-class>com.sun.xml.ws.transport.http.servlet.WSServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>CalcolatriceService</servlet-name>
        <url-pattern>/calcolatrice</url-pattern>
    </servlet-mapping>
    
</web-app>
```

## 5. Aggiunta delle Librerie JAX-WS

### 5.1 Configurare le Librerie JAX-WS

1. Cliccate con il tasto destro sul progetto
2. Selezionate Properties > Java Build Path > Libraries
3. Cliccate su "Add Library..."
4. Selezionate "Server Runtime" e cliccate su "Next"
5. Selezionate il server Tomcat configurato in precedenza
6. Cliccate su "Finish"

### 5.2 Aggiungere le Librerie Metro (Implementazione JAX-WS)

1. Scaricate il pacchetto Metro da: https://javaee.github.io/metro/
2. Estraete il contenuto del pacchetto
3. Cliccate con il tasto destro sul progetto > Properties > Java Build Path > Libraries
4. Cliccate su "Add External JARs..."
5. Navigate fino alla cartella `lib` del pacchetto Metro estratto
6. Selezionate tutti i file JAR e aggiungeteli al progetto
7. Copiate i file JAR selezionati nella cartella WEB-INF/lib del vostro progetto

## 6. Creazione della Classe di Endpoint

### 6.1 Creare la Classe per l'Endpoint

1. Cliccate con il tasto destro sul package
2. Selezionate New > Class
3. Assegnate un nome alla classe (es. "CalcolatriceEndpoint")
4. Cliccate su "Finish"
5. Implementate la classe di endpoint:

```java
package it.scuola.webservice;

import javax.xml.ws.Endpoint;

public class CalcolatriceEndpoint {
    
    // Metodo per avviare il servizio web
    protected void start() {
        // Crea un'istanza del servizio
        CalcolatriceService service = new CalcolatriceService();
        
        // Pubblica il servizio all'indirizzo specificato
        String address = "http://localhost:8080/calcolatrice";
        Endpoint.publish(address, service);
        
        System.out.println("Servizio avviato all'indirizzo: " + address);
        System.out.println("WSDL disponibile all'indirizzo: " + address + "?wsdl");
    }
    
    public static void main(String[] args) {
        // Avvia il servizio
        new CalcolatriceEndpoint().start();
    }
}
```

## 7. Deployment del Web Service

### 7.1 Creare il file sun-jaxws.xml

1. Cliccate con il tasto destro sulla cartella WEB-INF
2. Selezionate New > File
3. Nominate il file "sun-jaxws.xml"
4. Cliccate su "Finish"
5. Inserite il seguente contenuto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<endpoints xmlns="http://java.sun.com/xml/ns/jax-ws/ri/runtime" version="2.0">
    <endpoint name="CalcolatriceService"
              implementation="it.scuola.webservice.CalcolatriceService"
              url-pattern="/calcolatrice" />
</endpoints>
```

### 7.2 Deployment sul Server Tomcat

1. Cliccate con il tasto destro sul progetto
2. Selezionate Run As > Run on Server
3. Selezionate il server Tomcat configurato in precedenza
4. Cliccate su "Finish"

## 8. Test del Web Service

### 8.1 Utilizzare un Client SOAP per testare il servizio

1. Il WSDL del vostro servizio sarà disponibile all'indirizzo:
   `http://localhost:8080/SoapWebServiceDemo/calcolatrice?wsdl`

2. Per testare il servizio potete utilizzare:
   - SoapUI (applicazione gratuita per il test dei servizi SOAP)
   - Postman (con la funzionalità di richieste SOAP)
   - Un client Java personalizzato (vedi passo successivo)

### 8.2 Creare un Client Java per il Test

1. Cliccate con il tasto destro sul package
2. Selezionate New > Class
3. Assegnate un nome alla classe (es. "CalcolatriceClient")
4. Cliccate su "Finish"
5. Implementate il client:

```java
package it.scuola.webservice;

import java.net.URL;
import javax.xml.namespace.QName;
import javax.xml.ws.Service;

public class CalcolatriceClient {
    public static void main(String[] args) {
        try {
            // URL del WSDL
            URL wsdlURL = new URL("http://localhost:8080/SoapWebServiceDemo/calcolatrice?wsdl");
            
            // Namespace e nome del servizio
            QName qname = new QName("http://webservice.scuola.it/", "CalcolatriceService");
            
            // Creazione del servizio
            Service service = Service.create(wsdlURL, qname);
            
            // Ottenere l'interfaccia per il servizio
            CalcolatriceService calcolatrice = service.getPort(CalcolatriceService.class);
            
            // Test delle operazioni
            System.out.println("Somma 10 + 5 = " + calcolatrice.somma(10, 5));
            System.out.println("Sottrazione 10 - 5 = " + calcolatrice.sottrazione(10, 5));
            System.out.println("Moltiplicazione 10 * 5 = " + calcolatrice.moltiplicazione(10, 5));
            System.out.println("Divisione 10 / 5 = " + calcolatrice.divisione(10, 5));
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Nota: Per eseguire correttamente questo client, sarà necessario generare le classi client dal WSDL utilizzando lo strumento wsimport o utilizzare un'interfaccia condivisa.

## 9. Risoluzione dei Problemi Comuni

### 9.1 Errori di Dipendenza

Se incontrate errori relativi alle dipendenze JAX-WS, assicuratevi di:
- Aver aggiunto tutte le librerie necessarie
- Controllare che le librerie siano nella corretta versione
- Verificare che non ci siano conflitti tra le librerie

### 9.2 Errori di Connessione

Se il servizio non è raggiungibile:
- Controllate che Tomcat sia avviato correttamente
- Verificate che il mapping URL nel file web.xml sia corretto
- Controllate eventuali errori nei log di Tomcat

### 9.3 Errori WSDL

Se il WSDL non è generato correttamente:
- Controllate le annotazioni nella classe del servizio
- Verificate che i tipi di dati utilizzati siano supportati

## 10. Conclusione

Congratulazioni! Avete creato con successo un web service SOAP utilizzando Java ed Eclipse. Questo esempio di base può essere ampliato aggiungendo più funzionalità e gestendo casi d'uso più complessi.

Ricordate che i servizi SOAP sono solo uno dei modi per creare web service. In progetti futuri, potreste voler esplorare anche i servizi REST, che offrono un approccio più leggero alla comunicazione tra sistemi.
