* This project is a sub-project of XRCLOUD (https://xrcloud.app), an open-source project that aimed to provide membership-based cloud services for Hubs' Room and Scene resources, by forking the [hubs](https://github.com/Hubs-Foundation) project from [BELIVVR](https://belivvr.com) and developing additional features. 
  * (Korean) 본 프로젝트는 [BELIVVR](https://belivvr.com)에서 [hubs](https://github.com/Hubs-Foundation) 프로젝트를 fork하여 추가 기능을 개발하고, Hubs의 Room, Scene의 자원들을 회원제로 별도의 회원제 클라우드로 서비스를 제공하는 것을 목표 했던 XRCLOUD(https://xrcloud.app) 오픈소스 프로젝트의 서브 프로젝트 입니다.

* This repository is forked from [dialog created by hubfoundation](https://github.com/Hubs-Foundation/dialog).
  * (Korean) 본 저장소는 [hubfoundation에서 만든 dialog](https://github.com/Hubs-Foundation/dialog)를 fork한 저장소입니다.

* Dialog was created as a sub-project of [hubs-all-in-one](https://github.com/belivvr/xrcloud/hubs-all-in-one/), a project that runs the hubs project created by BELIVVR on a single host. For detailed information about XRCLOUD, please refer to the [XRCLOUD project page](https://github.com/belivvr/xrcloud/blob/main/README.md).
  * (Korean) dialog는 BELIVVR 에서 만든 hubs프로젝트를 단일 호스트에서 실행하는 프로젝트 [hubs-all-in-one](https://github.com/belivvr/xrcloud/hubs-all-in-one/)의 서브 프로젝트로 만들었습니다. XRCLOUD의 상세한 설명은 [XRCLOUD 프로젝트 페이지](https://github.com/belivvr/xrcloud/blob/main/README_ko.md)를 참고 바랍니다.

* As of February 2025, BELIVVR is releasing this as open source (https://github.com/belivvr/xrcloud) as the company will not be proceeding with further development due to operational difficulties.
  * 2025년 2월, BELIVVR는 기업의 운영이 어려워 추가 개발을 진행하지 않으므로 오픈 소스(https://github.com/belivvr/xrcloud)로 공개 합니다.

* For additional inquiries, please contact the former CEO of BELIVVR, Luke Yang (fstory97@gmail.com).
  * (Korean) 추가 문의는 BELIVVR의 대표 였던 양병석 대표(fstory97@gmail.com)에게 문의 바랍니다.

  * (Korean) 아래는 fork할 당시 원본 README.md 입니다.


# Dialog
Mediasoup based WebRTC SFU for Mozilla Hubs.

## Development
1. Clone repo
2. In root project folder, `npm ci` (this may take a while).
3. Create a folder in the root project folder called `certs` if needed (see steps 4 & 5).
4. Add the ssl cert and key to the `certs` folder as `fullchain.pem` and `privkey.pem`, or set the path to these in your shell via `HTTPS_CERT_FULLCHAIN` and `HTTPS_CERT_PRIVKEY` respectively. You can provide these certs yourself or use the ones available in https://github.com/mozilla/reticulum/tree/master/priv (`dev-ssl.cert` and `dev-ssl.key`).

5. Add the reticulum permissions public key to the `certs` folder as `perms.pub.pem`, or set the path to the file in your shell via `AUTH_KEY`.

  * If using one of the public keys from hubs-ops (located in https://github.com/mozilla/hubs-ops/tree/master/ansible/roles/janus/files), you will need to convert it to standard pem format.    
    * e.g. for use with dev.reticulum.io:  `openssl rsa -in perms.pub.der.dev -inform DER -RSAPublicKey_in -out perms.pub.pem`

6. Start dialog with `MEDIASOUP_LISTEN_IP=XXX.XXX.XXX.XXX MEDIASOUP_ANNOUNCED_IP=XXX.XXX.XXX.XXX npm start` where `XXX.XXX.XXX.XXX` is the local IP address of the machine running the server. (In the case of a VM, this should be the internal IP address of the VM).
  * If you choose to set the paths for `HTTPS_CERT_FULLCHAIN`, `HTTPS_CERT_PRIVKEY` and/or `AUTH_KEY` you may also define them inline here as well. e.g. 
  ```
  HTTPS_CERT_FULLCHAIN=/path/to/cert.file HTTPS_CERT_PRIVKEY=/path/to/key.file AUTH_KEY=/path/to/auth.key MEDIASOUP_LISTEN_IP=XXX.XXX.XXX.XXX MEDIASOUP_ANNOUNCED_IP=XXX.XXX.XXX.XXX npm start
  ```
     
7. Navigate to https://localhost:4443/ in your browser, and accept the self-signed cert.

8. You may now point Hubs/Reticulum to use `localhost:4443` as the WebRTC host/port.`

See `config.js` for all available configuration options.
