# Liveness, Readiness and Startup Probes

kubelet은 pod의 상태를 진단하기 위해 probe를 사용합니다.

## Handler

진단을 수행하기 위해 kubelet은 컨테이너에 의해서 구현된 핸들러를 호출합니다. 핸들러는 3가지 타입이 있습니다.

- ExecAction: 컨테이너 내에서 지정된 명령어를 실행합니다. 명령어 실행 결과의 exit code가 0이면 성공으로 간주합니다.
- TCPSocketAction: 컨테이너의 지정된 포트로 TCP 소켓 검사를 수행합니다. 포트가 활성화되어 있다면 성공으로 간주합니다.
- HTTPGetAction: 컨테이너의 지정된 포트 및 경로로 HTTP Get 요청을 수행합니다. 응답 status code가 2xx, 3xx일 경우 성공으로 간주합니다.

## Probe

진단을 수행하는 probe도 3가지 타입으로 나뉩니다.

- livenessProbe: 컨테이너가 현재 동작 중인지의 여부를 나타낸다. 만약 livenessProbe가 실패할 경우, 해당 컨테이너는 재시작 처리된다.
  - livenessProbe는 컨테이너 내부에서 실행되는 프로세스의 교착 상태를 파악하는 데 유용합니다.
  - 일반적인 오류로 인한 application shutdown 등은 pod의 restartPolicy 등을 통해 핸들링할 수 있지만, 컨테이너가 죽지 않으면서 동작하지 않는 교착 상태에 빠질 가능성이 있을 때에는 livenessProbe의 사용을 검토해야 합니다.
- readinessProbe: 컨테이너가 요청을 처리할 준비가 되었는지의 여부를 나타낸다. readinessProbe가 실패할 경우, 해당 pod과 연관된 모든 서비스들의 엔드포인트에서 pod의 IP 주소가 제거된다.
  - readinessProbe는 컨테이너 내부의 프로세스(일반적으로는 애플리케이션)가 외부 트래픽을 받아 처리할 준비가 되었는지를 판단할 수 있습니다.
  - 일반적인 사용자 요청을 가정하고 이 시간 내에, 이 정도의 retry 내에서는 요청이 처리가 되어야 한다는 기준이 있다면, 해당 기준을 적용해서 적절하게 요청을 처리할 수 없는 pod를 service endpoint에서 제거할 수 있습니다.
- startupProbe: 컨테이너 내의 애플리케이션이 시작되었는지를 나타낸다. startupProbe가 성공할 때까지 livenessProbe, readinessProbe는 활성화되지 않는다. startupProbe가 실패할 경우, 해당 컨테이너는 재시작 처리된다.
  - `initialDelay + failureThreshold * periodSeconds` 만큼의 시간 동안 startupProbe가 성공하지 못하면 pod가 재시작되고, 성공한다면 이후의 livenessProbe, readinessProbe가 활성화됩니다.

## Reference

- https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
- https://medium.com/finda-tech/kubernetes-pod%EC%9D%98-%EC%A7%84%EB%8B%A8%EC%9D%84-%EB%8B%B4%EB%8B%B9%ED%95%98%EB%8A%94-%EC%84%9C%EB%B9%84%EC%8A%A4-probe-7872cec9e568
- https://wrynn.tistory.com/47
