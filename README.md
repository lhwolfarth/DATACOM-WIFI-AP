# Portal Cativo Externo para APs Datacom


Fluxo do portal cativo:
 
Etapa 1: /login: do dispositivo do usuário para o portal cativo. O portal responde com um token. Pode exibir a página inicial do portal cativo.
 
Etapa 2: /auth: do ponto de acesso para o portal cativo para verificar o token. O portal verifica o token respondendo com Auth:1. Isso ocorre na porta TCP 80, mesmo que o portal cativo esteja usando HTTPS na porta 443. Portanto, a porta 80 também precisa estar aberta para responder a essa solicitação.
 
Etapa 3: /portal: do dispositivo do usuário para o portal cativo. Pode exibir a tela final do portal cativo que o usuário vê antes da autorização.
 
Logs de acesso do Apache:
 
154.192.47.15 - - [11/Fev/2025:06:50:00 +0000] "GET /login/?gw_id=G1RP6TP081524&gw_sn=G1RP6TP081524&gw_address=1.2.3.4&gw_port=2060&ip=192.168.200.29&mac=a2:8f:4f:10:27:5c&apmac=7085.c4d2.3e6f&ssid=Ruijie&url=http%3A%2F%2Fconnectivitycheck.gstatic.com%2Fgenerate_204&vlanid=1 HTTP/1.1" 302 4073 "http://connectivitycheck.gstatic.com/" "Mozilla/5.0 (Linux; Android 14; SM-A336E Build/UP1A.231005.007; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/132.0.6834.163 Mobile Safari/537.36"

154.192.47.15 - - [11/Fev/2025:06:50:01 +0000] "GET /auth/?gw_sn=G1RP6TP081524&gw_id=G1RP6TP081524&stage=login&ip=192.168.200.29&mac=a2:8f:4f:10:27:5c&token=a2:8f:4f:10:27:5c&incoming=0&outgoing=0&vlanid=1 HTTP/1.1" 301 918 "-" "MCFi 1.0.0"

154.192.47.15 - - [11/Fev/2025:06:50:02 +0000] "GET /portal/?gw_sn=G1RP6TP081524&gw_id=G1RP6TP081524&mac=a2:8f:4f:10:27:5c HTTP/1.1" 200 831 "http://connectivitycheck.gstatic.com/" "Mozilla/5.0 (Linux; Android 14; SM-A336E Build/UP1A.231005.007; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/132.0.6834.163 Mobile Safari/537.36"
 
O AP faz periodicamente uma solicitação /auth para registrar o heartbeat com o servidor do portal. O servidor pode responder com um Auth:0 sempre que o usuário precisar ser desautorizado.
