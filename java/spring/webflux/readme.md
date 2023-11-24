###basic concepts

#### WebFluxAutoConfiguration
```
all web flux related beans will be automatically created via this configuration bean
```
#### WebHttpHandlerBuilder
```
This builder has two purposes:

<p>One is to assemble a processing chain that consists of a target {@link WebHandler},
then decorated with a set of {@link WebFilter WebFilters}, then further decorated with
a set of {@link WebExceptionHandler WebExceptionHandlers}.

<p>The second purpose is to adapt the resulting processing chain to an {@link HttpHandler}:
the lowest-level reactive HTTP handling abstraction which can then be used with any of the
supported runtimes. The adaptation is done with the help of {@link HttpWebHandlerAdapter}.

<p>The processing chain can be assembled manually via builder methods, or detected from
a Spring {@link ApplicationContext} via {@link #applicationContext}, or a mix of both.
```
#### ServerWebExchange
```
Contract for an HTTP request-response interaction. Provides access to the HTTP
request and response and also exposes additional server-side processing
related properties and features such as request attributes.
```
#### WebFilter
```
like servelet filter used to implement global leve concerns,
e.g. request logging,authentication/authorization
```

#### CorsWebFilter
```
{@link WebFilter} that handles CORS preflight requests and intercepts
CORS simple and actual requests thanks to a {@link CorsProcessor} implementation
({@link DefaultCorsProcessor} by default) in order to add the relevant CORS
response headers (like {@code Access-Control-Allow-Origin}) using the provided
{@link CorsConfigurationSource} (for example an {@link UrlBasedCorsConfigurationSource}
instance.

<p>This is an alternative to Spring WebFlux Java config CORS configuration,
mostly useful for applications using the functional API.
```
#### WebExceptionHandler
```
Contract for handling exceptions during web server exchange processing.

```
### WebHandler

```
Contract to handle a web request.
```

### DispatcherHandler
```
Central dispatcher for HTTP request handlers/controllers. Dispatches to
registered handlers for processing a request, providing convenient mapping
facilities.

<p>{@code DispatcherHandler} discovers the delegate components it needs from
Spring configuration. It detects the following in the application context:
<ul>
<li>{@link HandlerMapping} -- map requests to handler objects
<li>{@link HandlerAdapter} -- for using any handler interface
<li>{@link HandlerResultHandler} -- process handler return values
</ul>

<p>{@code DispatcherHandler} is also designed to be a Spring bean itself and
implements {@link ApplicationContextAware} for access to the context it runs
in. If {@code DispatcherHandler} is declared as a bean with the name
"webHandler", it is discovered by
{@link WebHttpHandlerBuilder#applicationContext(ApplicationContext)} which
puts together a processing chain together with {@code WebFilter},
{@code WebExceptionHandler} and others.

<p>A {@code DispatcherHandler} bean declaration is included in
{@link org.springframework.web.reactive.config.EnableWebFlux @EnableWebFlux}
configuration.

DispatcherHandler processes requests as follows:

1.Each HandlerMapping is asked to find a matching handler, and the first match is used.

2.If a handler is found, it is run through an appropriate HandlerAdapter,
 which exposes the return value from the execution as HandlerResult.

3.The HandlerResult is given to an appropriate HandlerResultHandler 
to complete processing by writing to the response directly or by using a view to render
```

### WebSessionManager
```
The manager for WebSession instances exposed through a method on ServerWebExchange.
 DefaultWebSessionManager by default.
```
### ServerCodecConfigurer
```
For access to HttpMessageReader instances for parsing form data and multipart data 
that is then exposed through methods on ServerWebExchange. 
ServerCodecConfigurer.create() by default.
```
### LocaleContextResolver
```
The resolver for LocaleContext exposed through a method on ServerWebExchange.
 AcceptHeaderLocaleContextResolver by default.
```
### HandlerResultHandler
```
Process the {@link HandlerResult}, usually returned by an {@link HandlerAdapter}.
- ResponseEntityResultHandler  Handles {@link HttpEntity} and {@link ResponseEntity} return values.
- ServerResponseResultHandler Handles {@link ServerResponse ServerResponses}.
- ResponseBodyResultHandler that handles return values from methods annotated with {@code @ResponseBody}
- ViewResolutionResultHandler  encapsulates the view resolution algorithm
```
###