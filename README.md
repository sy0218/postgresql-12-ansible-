# postgresql 12 자동 설치 및 설정 setup 앤서블

## 필수 준비

- **필수 셋팅**: `system_download.txt 파일 /data/work 하위에 위치 필수!!!!`

## 참조 파일

- **셋업 참조 파일**: `system_download.txt(/data/work 하위에 위치 필수!!!!)`
- **postgresql 초기 설정 파일 샘플**: `pg_hba.conf`, `postgresql.conf`
- **전체 파이프라인 플레이북**: `postgresql_deploy.yml`

## 각 파일 설명

1. **`hosts.ini`** : 인벤토리(관리 대상 시스템 리스트)
2. **`main.yml`** : play_book 변수를 담은 파일
3. **`pg_hba.conf`, `postgresql.conf`** : postgresql 초기 설정 파일
5. **`entrypoint.sh`** : 초기 설정 파일 동적 setup
6. **`postgresql_deploy.yml`** : 앤서블 플레이북

## 실행 방법

1. `zpostgresql_deploy.yml` 플레이북을 실행하여 전체 파이프라인을 시작합니다.
   ```sh
   ansible-playbook -i /data/work/postgresql_12_auto_ansible/hosts.ini /data/work/postgresql_12_auto_ansible/postgresql_deploy.yml
   ```

## ansible 플레이북 구조

- `download Package postgresql`: postgresql 패키지 설치
- `postgresql make data_dir,init and conf_file cp`: entrypoint.sh 스크립트 실행 및 동적 setup된 설정 파일 working 디렉토리에 복사
- `postgresql service restart`: postgresql 서비스 시작

---

이 플레이북은 postgresql 를 자동으로 설정하고 Start 하는 과정을 자동화 합니다.
