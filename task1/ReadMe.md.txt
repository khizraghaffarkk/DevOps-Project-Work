docker build -t docker-registry.rahti.csc.fi/finalprojecttask1/f1demo2val:1.0 -f D:/check/test/pwtask1/f1demo2val/Dockerfile .

docker build -t docker-registry.rahti.csc.fi/finalprojecttask1/f1demo2val:1.0 -f Dockerfile .
docker push docker-registry.rahti.csc.fi/finalprojecttask1/f1demo2val:1.0

docker build -t docker-registry.rahti.csc.fi/finalprojecttask1/val2mqtt:1.0 -f Dockerfile .
docker push docker-registry.rahti.csc.fi/finalprojecttask1/val2mqtt:1.0



docker-compose up


mosquitto_sub -t "khghaffa23/#" --cafile ca.crt --insecure --host mqtt.khghaffa23.rahtiapp.fi --port 443 -v

mosquitto_sub -t "khghaffa23/#" --cafile D:\check\test\module\task1\val2mqtt\ca.crt --insecure --host mqtt.khghaffa23.rahtiapp.fi --port 443 -v
























mosquitto_sub -h mqtt.khghaffa23.rahtiapp.fi -p 443 --cafile ca.crt -t "khghaffa23/#"

mosquitto_sub -h mqtt.khghaffa23.rahtiapp.fi -p 443 --cafile D:\check\test\pwtask1\val2mqtt\ca.crt -t "khghaffa23/#"
