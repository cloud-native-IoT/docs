Here you find some notes about device certificate creation

## Certificate Creation Mode
At present, recasta supports only X509 certificate authentication for devices.

Generate a **private key** for the device:

openssl genrsa -out {key_filename}.key 4096

Generate the **client certificate** (and self-sign it):

openssl req -new -x509 -sha256 -key {key_filename}.key -out {crt_filename}.crt -days 365

To script the valid device certificates we developed a script which is used by our users:

```
FILENAME=$1
SIZE=$2

if [[ -n "$1" && -n "$2" ]]
then
    mkdir -p nodes; cd nodes
    openssl genrsa -out $FILENAME.key $SIZE
    openssl req -new -key $FILENAME.key -subj "/C=US/ST=TX/L=Dallas/O=recasta.cloud/OU=recasta/CN=$FILENAME" -out $FILENAME.csr
    openssl x509 -req -days 3650 -in $FILENAME.csr -CA ../CA.crt -CAkey ../CA.key -CAcreateserial -out $FILENAME.crt
else
    echo "Please set <filename> and <keysize> without extension for first argument without blank spaces.";
    echo "./cert.sh <filename> <keysize (eg 2048)>";
fi
```
Replace the key subjects accordingly to the desired ones.

**Note:**
The generated certificate key should be same as of the one used while device creation and while sending the mosquitto message [MQTT](Technical/MQTT.md) to the device.
.


