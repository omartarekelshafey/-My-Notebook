# How Web Applications Work

### How Web Applications Work

* Web works through the **HTTP protocol** (Layer 7 of OSI).
* Before HTTP, traffic passes through **Ethernet → IP → TCP → SSL**.
* Client (browser) sends an **HTTP Request** → server processes it → sends back an **HTTP Response** → browser displays the result.

***

### HTTP Requests

* Request must follow the **standard format** = Request line + Headers + Body.
* **Request line** → HTTP method (GET/POST…) + resource.
* **Important headers**:
  * **Host** → which domain.
  * **Cookie** → stores session info.
  * **Upgrade-Insecure-Requests** → ask to use SSL.
  * **User-Agent** → client’s browser/OS info.
  * **Accept** → type of data requested.
  * **Accept-Encoding** → compression supported.
  * **Accept-Language** → preferred language.
  * **Connection** → keep-alive or close.
* **Body** → contains data (e.g. POST parameters).

***

### HTTP Responses

* Server returns Response with:
  * **Status Line** → HTTP version + Status Code (200 OK, 404 Not Found…).
    * 100–199: Info.
    * 200–299: Success.
    * 300–399: Redirection.
    * 400–499: Client error.
    * 500–599: Server error.
  * **Headers**:
    * Date → when response sent.
    * Connection → how connection handled.
    * Server → server info.
    * Last-Modified → last update of resource.
    * Content-Type → type of data.
    * Content-Length → size of data.
  * **Body** → actual resource (HTML, JSON, image…).

***

