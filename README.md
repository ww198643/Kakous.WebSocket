# Kakous.WebSocket

### register middleware
```csharp
public void ConfigureServices(IServiceCollection services)
{
  services.AddKakousWebSocket();
  services.AddMvc();
}
public void Configure(IApplicationBuilder app, IHostingEnvironment env, IServiceProvider serviceProvider)
{
  if (env.IsDevelopment())
  {
    app.UseDeveloperExceptionPage();
  }

  app.UseMvc();
  app.UseKakousWebSocket("/sc/connect", serviceProvider.GetService<MyWebSocketHandler>());
}
```

### custom message handler
```csharp
public class MyWebSocketHandler : WebSocketHandler
{
  public MyWebSocketHandler(WebSocketsConnectionManager webSocketsConnectionManager) : base(webSocketsConnectionManager)
  {
  }

  public override string OnConnected(HttpContext context, WebSocket socket)
  {
    return base.OnConnected(context, socket);
  }

  public override async Task ReceiveAsync(WebSocket sender, string message)
  {
    await SendMessageToAllAsync("收到：" + message);
  }
}
```
