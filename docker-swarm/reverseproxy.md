server {
    listen 80;
    server_name n.example.com;
    
    # Redirect HTTP to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name n.example.com;

    ssl_certificate /etc/letsencrypt/live/n.example.com/fullchain.pem; # Adjust the path based on your cert location
    ssl_certificate_key /etc/letsencrypt/live/n.example.com/privkey.pem; # Adjust the path based on your cert location

    # Main location block
    location / {
        proxy_pass http://192.168.0.118:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Disable buffering for compatibility with Nextcloud file access
        proxy_buffering off;

        # Large file handling
        client_max_body_size 10G;
        proxy_max_temp_file_size 2048m;

        # Timeout settings for larger files
        proxy_connect_timeout 60s;
        proxy_send_timeout 60s;
        proxy_read_timeout 120s;
        send_timeout 120s;
    }

    # WebSocket support for Collabora Online
    location /loleaflet/ {
        proxy_pass http://192.168.0.118:9980; # Collabora's internal port
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /hosting/ {
        proxy_pass http://192.168.0.118:9980; # Collabora's internal port
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /loaf/ {
        proxy_pass http://192.168.0.118:9980; # Collabora's internal port
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
