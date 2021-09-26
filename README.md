# SocketIO
Web Socket client for .NET framework 4+ & Core

## Usage
* Import namespace
                `using SocketIOClient;`
* Declare variables  
                ```
                SocketIO client;
                SocketIOOptions SocketIOOptions;
                ```
* Assign Variables & Events
                
               SocketIOOptions = new SocketIOOptions
                {
                    Reconnection = true,
                    AllowedRetryFirstConnection = true,
                    ConnectionTimeout = TimeSpan.FromMinutes(3),
                    EIO = 4
                };
            
                client = new SocketIO("URL HERE", SocketIOOptions); 
                client.OnReconnectFailed += Client_OnReconnectFailed;
                client.OnReconnecting += Client_OnReconnecting;
                client.OnError += Client_OnError;
                client.OnPing += Client_OnPing;
                client.OnPong += Client_OnPong;
                client.OnConnected += Client_OnConnected;
                client.OnDisconnected += Client_OnDisconnected;
                client.OnReceivedEvent += Client_OnReceivedEvent;
        
        private void Client_OnReceivedEvent(object sender, SocketIOClient.EventArguments.ReceivedEventArgs e)
        {
            try
            { 
               Console.WriteLine(e.Event);
            }
            catch (Exception Ex)
            {
                Logger.Error(Ex); 
            }
        }

        private void Client_OnPong(object sender, TimeSpan e)
        {
            Console.WriteLine("PONG");
        }

        private void Client_OnPing(object sender, EventArgs e)
        {
            Console.WriteLine("PING");
        }
         
        private void Client_OnDisconnected(object sender, string e)
        {
             Console.WriteLine("DISCONNECTED");
        }

        private void Client_OnReconnectFailed(object sender, Exception e)
        {
             Console.WriteLine("RE-CONNECT FAILED");
        }

        private void Client_OnReconnecting(object sender, int e)
        {
            Console.WriteLine("RE-CONNECTING"); 
        }

        private void Client_OnConnected(object sender, EventArgs e)
        {
             var socket = sender as SocketIO;
             Console.WriteLine("CONNECTED WITH SOCKET ID = " + socket.Id);
        }

        private void Client_OnError(object sender, string e)
        {
             Console.WriteLine("ERROR"); 
        } 
* Call Connect Method to start listening your socket
                `client.ConnectAsync();`
