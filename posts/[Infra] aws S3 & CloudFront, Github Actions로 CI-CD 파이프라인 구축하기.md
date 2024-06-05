<h1 id="aws-s3">AWS S3</h1>
<p>👩‍🏫 S3를 이해하기 위해서는 우선 스토리지에 대한 이해가 필요합니다.</p>
<h2 id="클라우드-스토리지">클라우드 스토리지</h2>
<h3 id="클라우드-스토리지란">클라우드 스토리지란?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/e7a4741b-c401-4946-b688-8b5e438e48b3/image.png" /></p>
<ul>
<li>클라우드 컴퓨팅 제공 업체를 통해 데이터와 파일을 인터넷에 저장할 수 있는 클라우드 컴퓨팅 모델</li>
<li>확장성을 제공하여 필요에 따라 스토리지 용량을 빠르게 늘리거나 줄일 수 있다.</li>
<li>중복성을 제공하여 데이터 손실을 방지하기 위한 데이터 사본을 생성한다.</li>
<li>접근성을 제공하여 사용자는 퍼블릭 인터넷 또는 전용 프라이빗 네트워크 연결을 통해 언제 어디서나 인터넷에 연결된 모든 장치에서 데이터에 엑세스할 수 있다.</li>
</ul>
<h3 id="클라우드-스토리지의-유형">클라우드 스토리지의 유형</h3>
<p><a href="https://www.smileshark.kr/post/amazon-s3-efs-ebs-which-aws-storage-service-to-use"><img src="https://velog.velcdn.com/images/hamjw0122/post/c8631549-76a4-4c0f-a4db-5529e9fd8618/image.png" /></a></p>
<blockquote>
<p>블록 스토리지</p>
</blockquote>
<p><a href="https://www.smileshark.kr/post/amazon-s3-efs-ebs-which-aws-storage-service-to-use"><img src="https://velog.velcdn.com/images/hamjw0122/post/867714ef-52d7-433d-a379-5b27526b6ec9/image.png" /></a></p>
<ul>
<li>데이터를 일정한 크기의 <strong>블록</strong>으로 나누어 저장하는 방식</li>
<li>각각의 블록은 고유한 주소를 가지며, 이를 통해 블록을 재구성하여 데이터를 불러올 수 있다.<ul>
<li>컴퓨터 드라이브에 파티션을 나눠 공간을 사용하는 것과 유사한 개념이다.</li>
</ul>
</li>
<li>정형화된 데이터를 빠르게 처리하는 데 이상적이다.</li>
<li>고유한 주소가 있으므로 다양한 접근 경로를 가진다. ➡️ 신속한 검색이 가능하다.</li>
<li>파티션 분할이 가능하므로 서로 다른 OS에서의 접근이 가능하다.</li>
<li>블록 단위로 분할하여 저장하므로 스토리지 자체적으로 읽기/쓰기 등의 기능 수행이 불가능하다.</li>
<li>메타데이터를 관리하기 위한 수단이 제한적이다. </li>
<li>AWS의 블록 스토리지 서비스: <a href="https://aws.amazon.com/ko/ebs/"><strong><em>EBS(Elastic Block Store)</em></strong></a><ul>
<li>Amazon EC2 인스턴스에서 사용하는 고성능 블록 스토리지 서비스</li>
<li>영구 블록 스토리지 볼륨을 제공하여 EC2 인스턴스가 종료되어도 데이터가 날아가지 않는다.</li>
<li>사용자가 원하는 성능 제공이 가능하다.</li>
<li>DB, 파일 시스템 또는 원시 블록 수준 스토리지에 대한 액세스가 필요한 경우 적합하다.</li>
<li>단일 인스턴스에 대한 고성능 스토리지 서비스가 필요한 경우 사용한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>파일 (기반) 스토리지</p>
</blockquote>
<p><a href="https://www.smileshark.kr/post/amazon-s3-efs-ebs-which-aws-storage-service-to-use"><img src="https://velog.velcdn.com/images/hamjw0122/post/9f5adf7f-d48d-44ff-8f3c-4f62d52d280c/image.png" /></a></p>
<ul>
<li>폴더와 파일로 이뤄진 계층 구조를 가지고 있다.</li>
<li>각 파일은 폴더에 종속되며, 해당 폴더는 다시 다른 폴더에 종속될 수 있다.<ul>
<li>윈도우 탐색기와 유사한 개념이다. (폴더 내부에 폴더, 내부에 파일 저장)</li>
</ul>
</li>
<li>파일/폴더 만으로 구성된 구조로 파일에 대한 정보 외의 부가적인 데이터(메타데이터) 저장에 제한적이다.</li>
<li>파일을 찾으려면 해당 파일의 경로를 알아야 한다.<ul>
<li>파일이 많을 경우 분류, 정리, 검색이 불편할 수 있다.</li>
<li>데이터 양이 늘어나면서 파일과 폴더를 계속 추적하기 위한 자원 요구가 늘어나 성능이 떨어질 수 있다.</li>
</ul>
</li>
<li>AWS의 파일 스토리지 서비스: <a href="https://aws.amazon.com/ko/efs/"><strong><em>EFS(Elastic File System)</em></strong></a><ul>
<li>AWS 클라우드 서비스 및 온프레미스 리소스와 함께 사용할 수 있는 간단하고 확장 가능한 서버리스 파일 시스템</li>
<li>수천 개의 EC2에서 동시에 엑세스 가능하다.</li>
<li>파일이 추가 또는 제거됨에 따라 자동으로 스토리지 용량을 즉시 확장하거나 축소한다.</li>
<li>여러 가용 영역에 파일이 중복 저장되어 하나의 가용 영역이 파괴되더라도 다른 가용 영역에서 서비스를 제공할 수 있다.</li>
<li>지속적으로 공유되고 빈번한 읽기/쓰기가 필요한 경우 적합하다.</li>
<li>여러 EC2 인스턴스에 대한 공유 파일 시스템이 필요한 workdload에 적합하다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>객체 스토리지</p>
</blockquote>
<p><a href="https://www.smileshark.kr/post/amazon-s3-efs-ebs-which-aws-storage-service-to-use"><img src="https://velog.velcdn.com/images/hamjw0122/post/2c933c53-d671-47cb-9641-5ae0381a32f6/image.png" /></a></p>
<ul>
<li>각 데이터 조각을 객체로 지정하고 개별 데이터 단위로 저장한다.<ul>
<li>객체: 비정형 데이터(사진, 비디오) + 기계 학습(ML) + 센서 데이터 등의 모든 데이터</li>
</ul>
</li>
<li>계층 구조가 없는 평면적 공간에 데이터를 저장한다.<ul>
<li>공간에는 고유 식별자가 있고 객체는 객체 자체로 저장되어 접근성이 좋다.</li>
<li>객체의 키만 알면 쉽고 빠른 검색이 가능하다.</li>
<li>접근이 쉽고 빠르며 확장성이 높다.</li>
</ul>
</li>
<li>논리적인 스토리지<ul>
<li>블록 스토리지와 파일 스토리지는 모두 OS 단에서 동작하지만 객체 스토리지는 어플리케이션 단에서 동작한다.</li>
<li>물리적 제약이 없어 원하는 만큼 공간 확장이 가능하다.</li>
</ul>
</li>
<li>스토리지 자체 권한 관리가 가능하며 개별 객체마다 권한을 부여할 수 있다.</li>
<li>AWS의 객체 스토리지 서비스: <a href="https://aws.amazon.com/ko/s3/"><strong><em>S3(Simple Storage Service)</em></strong></a><ul>
<li>인터넷 엑세스가 가능한 객체 스토리지 서비스</li>
<li>구글 드라이브, 아이클라우드처럼 온라인으로 데이터를 저장하는 서비스</li>
<li>확장성, 내구성, 가용성이 뛰어나다.</li>
<li>자주 열어보지 않을 사내 공유 문서 및 복잡한 쿼리를 실행할 수 있는 데이터 저장에 유용하다.</li>
<li>정적 웹사이트를 지원하여 여러 개의 정적 HTML 페이지를 호스팅해야 할 경우 사용 가능하다. </li>
</ul>
</li>
</ul>
<h2 id="aws-s3란">AWS S3란?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/5330a01e-53e4-4aac-9a71-91957cf96ed3/image.png" /></p>
<ul>
<li><p><strong><em>Simple Storage Service</em></strong>의 약자로 AWS에서 제공하는 클라우드 기반 객체 스토리지 서비스이다.</p>
</li>
<li><p>저장되는 객체마다 독립적인 접근 경로, 권한, 메타데이터를 제공 및 구성할 수 있다.</p>
</li>
<li><p>많은 사용자가 접속하더라도 이를 감당하기 위한 별도의 시스템적 작업을 할 필요가 없다.</p>
</li>
<li><p>저장할 수 있는 파일 수에 제한이 없다.</p>
</li>
<li><p>최소 1byte에서 최대 5TB의 데이터를 저장하고 서비스할 수 있다.</p>
</li>
<li><p>기본적으로 public access가 차단되고, 개발자가 원하는 경우 객체 단위로 접근을 허용할 수 있다.</p>
<ul>
<li>객체 암호화 기능을 통해 객체가 노출되더라도 읽을 수 없게 조치할 수 있다. </li>
</ul>
</li>
<li><p>HTTP와 BitTorrent 프로토콜을 지원한다.</p>
<table>
<thead>
<tr>
<th align="center">HTTP</th>
<th align="center">Bitorrent</th>
</tr>
</thead>
<tbody><tr>
<td align="center">HTML과 같은 하이퍼미디어 문서를 전송하기 위한 <br /> 애플리케이션 계층 프로토콜</td>
<td align="center">P2P 파일 전송 프로토콜이자 응용 소프트웨어. <br /> 파일을 인터넷 상에 분산하여 저장해두고 다수의 접속을 사용하여 <br /> 여러 곳에서 동시에 파일을 가져오게 되므로 전송 속도가 빨라진다.</td>
</tr>
</tbody></table>
</li>
<li><p>REST, SOAP 인터페이스를 제공한다.</p>
<table>
<thead>
<tr>
<th align="center">REST</th>
<th align="center">SOAP</th>
</tr>
</thead>
<tbody><tr>
<td align="center">Representational State Transfer</td>
<td align="center">Simple Object Access Protocol</td>
</tr>
<tr>
<td align="center">통신 인터페이스 설계를 위한 아키텍쳐 스타일</td>
<td align="center">애플리케이션 간 통신을 위한 프로토콜</td>
</tr>
<tr>
<td align="center">HTTPS에서만 작동한다.</td>
<td align="center">독립적이며 모든 전송 프로토콜과 함께 작동할 수 있다.</td>
</tr>
<tr>
<td align="center">XML, JSON, 일반 텍스트, HTML 데이터를 지원한다.</td>
<td align="center">XML 데이터 교환만 지원한다.</td>
</tr>
<tr>
<td align="center">작은 메시지, caching 지원으로 성능이 빠르다.</td>
<td align="center">메시지가 커 통신 속도가 느려진다.</td>
</tr>
<tr>
<td align="center">무상태 방식이므로 확장하기 쉽다. <br /> 모든 메시지가 이전 메시지와 독립적으로 처리된다.</td>
<td align="center">확장하기 어렵다. <br /> 서버는 클라이언트와 교환한 이전 메시지를 <br /> 모두 저장해 상태를 유지한다.</td>
</tr>
<tr>
<td align="center">성능에 영향을 주지 않고 암호화를 지원한다.</td>
<td align="center">추가 overhead가 있는 암호화를 지원한다.</td>
</tr>
<tr>
<td align="center">최신 애플리케이션, Open API에 유용하다.</td>
<td align="center">legacy 애플리케이션 및 private API에서 유용하다.</td>
</tr>
</tbody></table>
</li>
<li><p>버전 관리 기능을 통해 사용자에 의한 실수를 복원할 수 있다.</p>
</li>
<li><p>정보의 중요도에 따라 보호 수준을 차등 지정하여 비용을 절감할 수 있다.</p>
</li>
</ul>
<h2 id="aws-s3의-기본-용어-알기">AWS S3의 기본 용어 알기</h2>
<h3 id="객체-object">객체 (Object)</h3>
<ul>
<li>S3에 저장된 데이터 하나 하나 (각각의 파일이라고 생각하면 된다.)</li>
</ul>
<h3 id="버킷-bucket"><a href="https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/UsingBucket.html">버킷 (Bucket)</a></h3>
<ul>
<li>S3에 저장된 객체에 대한 컨테이너</li>
<li>연관된 객체들을 grouping한 최상위 디렉토리</li>
<li>스토리지 구성에 따라 하나의 버킷에 여러 종류의 파일을 저장할 수도 있고 파일의 종류별로 버킷을 분리할 수도 있다.</li>
<li>버킷 단위로 region을 지정할 수 있고, 버킷에 포함된 모든 객체에 대해 일괄적으로 인증 및 접속 제한을 걸 수 있다.</li>
</ul>
<h3 id="버킷-버전-관리"><a href="https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/Versioning.html">버킷 버전 관리</a></h3>
<ul>
<li>S3에 저장된 객체들의 변화를 저장하는 것을 의미한다.</li>
<li>사용자가 객체를 삭제하거나 변경하더라도 각각의 변화를 모두 기록하므로 실수를 복원할 수 있다.</li>
</ul>
<h3 id="acl-access-control-list"><a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/acls.html">ACL (Access Control List)</a></h3>
<ul>
<li>ACL을 활성화할 경우 객체에 대한 접근 권한을 내 계정이 아닌 다른 계정에게도 부여할 수 있다.</li>
<li>특별한 경우가 아니라면 비활성화하는 것이 권장된다. </li>
</ul>
<h3 id="리전-region"><a href="https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-regions.html">리전 (Region)</a></h3>
<ul>
<li>사용자가 만드는 버킷을 저장할 지리적 AWS 리전</li>
<li>지연시간 최적화, 비용 최소화, 규정 요구 사항 준수 등의 기준에 따라 선택할 수 있다.</li>
<li>AWS 리전에 저장된 객체는 사용자가 명시적으로 다른 리전으로 객체를 전송하거나 복제하지 않는 한 해당 리전을 벗어나지 않는다.</li>
<li>계정에 대해 사용되는 AWS 리전에서만 Amazon S3에 접근하고 해당 기능을 사용할 수 있다.</li>
</ul>
<h3 id="rss-reduced-redundancy-storage">RSS (Reduced Redundancy Storage)</h3>
<ul>
<li>일반 S3 객체에 비해 데이터가 손실될 확률이 높은 형태의 저장 방식</li>
<li>그러나 일반 S3 객체에 비해 가격이 저렴하므로 복원 가능한 데이터(예: 썸네일 이미지) 등을 저장하기에 적합하다.</li>
</ul>
<h3 id="s3-glacier"><a href="https://aws.amazon.com/ko/s3/storage-classes/glacier/">S3 Glacier</a></h3>
<ul>
<li>매우 저렴한 가격으로 데이터를 저장할 수 있는 AWS의 스토리지 서비스 </li>
<li>자주 사용하지 않는 데이터를 S3 Glacier에 저장하면 매우 적은 비용으로 클라우드 내 데이터 보관이 가능하다. </li>
</ul>
<h1 id="aws-cloudfront">AWS CloudFront</h1>
<h2 id="cdn-content-delivery-network">CDN (Content Delivery Network)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/eae301c7-671c-40c0-8a09-72eb91f4691f/image.png" /></p>
<h3 id="cdn이란">CDN이란?</h3>
<ul>
<li>지리적 제약 없이 전 세계 사용자에게 빠르고 안전하게 콘텐츠를 전송할 수 있도록 하는 콘텐츠 전송 기술</li>
<li>콘텐츠를 효율적으로 전달하기 위해 여러 노드를 가진 네트워크에 데이터를 저장하여 제공하는 시스템</li>
<li>전세계에 골고루 캐시 서버(PoP)를 분산 배치하여 서버와 사용자 간의 물리적인 거리를 줄인다.<ul>
<li>이를 통해 컨텐츠를 불러오는 데 소요되는 시간을 최소화한다.</li>
<li>예를 들어, 미국 사용자가 한국에 호스팅 된 웹 사이트에 접근할 경우 미국에 위치한 PoP 서버에서 웹 사이트 콘텐츠를 사용자에게 전송한다.</li>
</ul>
</li>
<li>ISP(Internet Service Provider, 인터넷 서비스 제공자)에 직접 연결되어 데이터를 전송하므로 데이터 병목을 피할 수 있다.</li>
</ul>
<h3 id="cdn의-특징">CDN의 특징</h3>
<ul>
<li>콘텐츠를 보다 빠르게 전송하므로 속도 개선과 회선 비용 절감에 용이하다.</li>
<li>최초 요청 시 서버로부터 콘텐츠를 가져와 고객에게 전송함과 동시에 CDN caching 장비에 저장한다.<ul>
<li>이후에는 해당 장비에 저장된 콘텐츠를 바로 전송하게 된다.</li>
</ul>
</li>
<li>CDN 업체에서 지정하는 컨텐츠 만료 지점까지 호출이 없을 경우 주기적으로 삭제한다.</li>
</ul>
<h2 id="aws-cloudfront란">AWS CloudFront란?</h2>
<ul>
<li>개발자 친화적 환경에서 짧은 지연 시간과 빠른 전송 속도로 데이터, 동영상, 어플리케이션 및 API를 전 세계 고객에게 안전하게 전송하는 고속 CDN 서비스이다.</li>
<li>AWS의 글로벌 인프라에 기반하여 데이터의 caching을 통해 실 사용자와 가장 가까운 서버에서 데이터를 전송해주는 글로벌 서비스이다.</li>
<li>전 세계의 AWS 센터에 CloundFront의 Edge Server가 배치되어 있다.<ul>
<li>사용자가 데이터를 요청할 때 사용자의 위치와 가장 가까운 Edge Server에서 데이터를 전달할 수 있다.</li>
</ul>
</li>
<li>일반적인 CDN과 같이 다운로드 방식과 스트리밍 방식을 모두 제공한다.</li>
<li>기본적으로 HTTP, HTTPS 프로토콜을 모두 지원하며, 스트리밍의 경우 RTS로도 제공 가능하다. </li>
<li>S3 같은 서비스에서 사용할 경우 가장 가까운 edge로 라우팅되어 콘텐츠 전송 속도를 향상시킬 수 있다.</li>
</ul>
<h3 id="aws의-edge-location">AWS의 Edge Location</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/78c158da-1cc0-42fb-9263-f2cf6c227e03/image.png" /></p>
<ul>
<li>AWS CDN들의 여러 서비스들을 가장 빠른 속도로 제공하기 위한 거점으로, 전 세계 여러 장소에 흩어져있다.<ul>
<li>정확하게는 AWS의 CDN 서비스인 CloudFront와 AWS의 DNS 서비스인 Route53의 캐시 서버를 의미한다.</li>
</ul>
</li>
<li>각 거점마다 가깝고 적당한 곳에 임시 데이터 저장소 센터인 edge location을 배치하여 더  빠르게 요청한 데이터를 저장할 수 있게 한다.</li>
<li>CloudFront를 통해 서비스하는 콘텐츠를 사용자가 요청할 경우 지연 시간이 가장 낮은 edge location으로 라우팅되므로 콘텐츠 성능이 뛰어나다.<ul>
<li>이때 콘텐츠가 이미 지연 시간이 가장 낮은 edge location에 있는 경우 CloudFront가 콘텐츠를 즉시 제공해준다.</li>
</ul>
</li>
</ul>
<h3 id="aws의-장점">AWS의 장점</h3>
<ul>
<li>AWS 네트워크를 사용할 경우 사용자의 요청이 반드시 통과해야 하는 네트워크의 수가 감소하여 성능이 향상된다.</li>
<li>파일의 첫 byte를 로드하는 데 소요되는 시간이 줄어들고 데이터 전송 속도가 빨라진다.</li>
<li>객체의 사본이 전 세계의 여러 edge location에 유지/cache 되므로 안정성과 가용성이 향상된다.</li>
<li>보안성 또한 향상된다.<ul>
<li>origin 서버에 대한 종단 간 연결의 보안이 보장된다. (HTTPS)</li>
<li>서명된 URL 및 cookie 사용 옵션으로 자체 사용자 지정 origin에 대해 private 콘텐츠를 제공하도록 할수도 있다. </li>
</ul>
</li>
</ul>
<h1 id="cicd-파이프라인-구축-경험">CI/CD 파이프라인 구축 경험</h1>
<h2 id="s3--cloudfront-조합을-선택하게-된-이유">S3 + CloudFront 조합을 선택하게 된 이유</h2>
<h3 id="ec2--nginx로-정적-사이트-배포하기">EC2 + Nginx로 정적 사이트 배포하기</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/341267b9-e1cd-40e9-8733-eb079fbd29f5/image.png" width="40%" />

<ul>
<li>AWS EC2 인스턴스 위에 Nginx 웹 서버를 배포하여 서버 호스팅을 진행한다.</li>
<li>EC2는 가상 서버로 기능하며, Nginx는 OS 위에 웹 서비스를 띄우기 위한 웹 서버가 된다.</li>
<li>👍 장점<ul>
<li>Nginx는 대용량 트래픽을 처리할 수 있도록 가볍고 높은 성능을 제공하는 경량 웹서버이므로 안정적인 성능으로 정적 파일 호스팅을 진행할 수 있다.</li>
<li>Nginx 환경을 직접 구성할 수 있게 되어 Nginx의 다른 기능들도 활용할 수 있다. (백엔드 서비스, Proxy 환경, 동적 페이지 구축 등)</li>
<li>하나의 웹 루트를 통해 여러 데모들을 관리하기에 용이하다.</li>
</ul>
</li>
<li>👎 단점<ul>
<li>관리를 위해 Nginx.conf 문법 및 Linux 기반 터미널 명령을 숙지해야 하므로 웹 서버를 관리할 서비스 관리자가 필요하다.</li>
<li>실제 EC2 서버가 있는 region이 아닌 지역의 클라이언트가 EC2 서버로 정적인 페이지를 요청할 경우 클라이언트와 서버 간의 물리적인 거리 때문에 응답 시간이 더 오래 걸릴 수 있다.</li>
<li>라우터를 사용하는 SPA 애플리케이션의 경우 추가적인 설정이 필요하다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>react-router-dom과 nginx</p>
</blockquote>
<ul>
<li>react-router-dom의 <code>BrowserRouter</code>를 통해 Single Page인 React 페이지에 경로를 주게 된다.</li>
<li><code>BrowserRouter</code>는 실제로 페이지를 불러오는 것이 아니다.<ul>
<li>대신 URL 주소가 바뀔 때 이를 바탕으로 컴포넌트를 렌더링하는 기능을 하기 위해 React 앱의 경로를 읽는 목적으로 React 내부에서 사용된다.</li>
</ul>
</li>
<li>따라서 웹 브라우저에서 경로를 변경한 후 브라우저 새로고침을 누르면 ⚠️<strong>404에러</strong>⚠️가 발생한다.<ul>
<li>router가 제공하는 것은 실제로 웹 리소스가 존재하는 경로가 아닌 React 내부의 경로이다.</li>
<li>이 때문에 위의 경우 <code>BrowserRouter</code>가 동작하기 전에 해당 경로로 웹 리소스 요청이 일어나게 되어 오류가 발생하는 것이다.</li>
</ul>
</li>
</ul>
<p>➡️ 이러한 문제를 해결하려면 Nginx로 들어오는 웹 요청의 경로를 실제 React SPA 앱의 <code>index.html</code>로 치환해주는 <code>try-files</code> 옵션 설정이 필요하다.</p>
<h3 id="s3--cloudfront로-정적-사이트-배포하기">S3 + CloudFront로 정적 사이트 배포하기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/d6ad5861-e176-4011-af07-1bec9e80b516/image.png" /></p>
<ul>
<li>Origin(S3)의 데이터를 CloudFront에서 Edge Server에 caching하고 caching된 데이터를 실 사용자에게 반환하는 구조이다.</li>
<li>데이터 caching을 위해 S3에서 데이터를 호출하는 경우 해당 caching에 사용되는 트래픽에는 비용이 청구되지 않는다.</li>
<li>👍 장점<ul>
<li>CDN 서비스이므로 여러 국가에서 서비스를 할 경우 안정적인 속도가 보장된다.</li>
<li>AWS console을 사용하여 편리하게 S3 업로드, edge location에서의 cache 무효화, 요청에 대한 redirection 처리 등의 작업을 처리할 수 있다.</li>
<li>서버를 직접 임대하는 것이 아니므로 서버 운용 비용이 아닌 실제 edge와 클라이언트 간 발생한 트래픽 만큼의 요금만 부과된다. (트래픽에 대한 과금은 EC2와 유사하다.)</li>
<li>S3의 특징으로 항상 고가용성 및 내구성을 보장한다.</li>
</ul>
</li>
<li>👎 단점<ul>
<li>초기 구축 시 S3와 CloudFront 설정에 대한 상세한 이해가 필요하다.</li>
<li>React와 같은 SPA 사이트 구축 시 403, 404 redirect 등의 추가 설정이 필요하다.</li>
<li>Nginx + EC2 배포처럼 여러 정적인 웹 사이트들을 호스팅 할 경우 버킷의 최상단 <code>index.html</code>만을 바라보게 되므로 S3 버킷의 서브 디렉터리에서 <code>index.html</code>을 생략할 수 없게 된다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>두 방식을 비교한 후 아래와 같은 이유로 S3 + CloudFront 조합을 사용하기로 결정했다.</strong></p>
</blockquote>
<ul>
<li>S3와 CloudFront를 사용할 경우 서버 인스턴스를 구성하지 않아도 되고 운영체제 및 소프트웨어 업데이트를 처리하지 않아도 된다.</li>
<li>S3와 CloudFront를 사용할 경우 트래픽이 급증할 때 서버 인스턴스를 수동으로 확장하고 <a href="https://aws.amazon.com/ko/what-is/load-balancing/">로드 밸런싱</a>을 구성하지 않아도 대응이 가능하다.</li>
<li>S3와 CloudFront를 사용할 경우 사용할 만큼만 비용을 지불하기 때문에 서버 인스턴스를 유지하기 위한 고정 비용이 발생하지 않으므로 비용이 더 적게 부과된다.</li>
<li>CoudFront는 전 세계의 엣지 로케이션에서 콘텐츠를 캐시하므로 사용자에게 더 빠르고 안정적인 서비스를 제공할 수 있을 것 같다.</li>
</ul>
<h2 id="s3--cloudfront로-정적-웹-사이트-배포하기">S3 + CloudFront로 정적 웹 사이트 배포하기</h2>
<h3 id="s3-버킷-생성하기">S3 버킷 생성하기</h3>
<p>S3 메뉴에서 버킷 만들기 버튼을 클릭한 뒤 버킷을 생성한다. </p>
<h4 id="1--사용하고자-하는-버킷의-이름을-지정해준다">1.  사용하고자 하는 버킷의 이름을 지정해준다.</h4>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/9a359806-7c3d-4d1b-9da2-1694818518e2/image.png" /></p>
<h4 id="2-퍼블릭-액세스-차단-설정을-진행한다">2. 퍼블릭 액세스 차단 설정을 진행한다.</h4>
<ul>
<li>S3에서 객체 주소를 가지고 누군가 직접 접속하더라도 콘텐츠가 차단되도록 막아준다. </li>
<li>CloudFront를 함께 쓰는 경우 가급적 <strong>모든 퍼블릭 액세스를 차단</strong>하는 것이 좋다고 한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2f40d553-9f75-4040-989d-114cbadb2331/image.png" /></li>
</ul>
<h4 id="3-정적-웹-사이트-호스팅을-위한-추가-설정을-진행한다">3. 정적 웹 사이트 호스팅을 위한 추가 설정을 진행한다.</h4>
<ul>
<li><code>속성</code> 탭 페이지 최하단의 <code>정적 웹 사이트 호스팅</code>에서 <code>편집</code> 버튼을 클릭해 정적 웹 사이트 호스팅을 <strong>활성화</strong>한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2148e76d-9137-45e7-abc2-cd4b519d773f/image.png" /></p>
<ul>
<li>인덱스 문서 파일명을 입력해준 뒤 <code>변경 사항 저장</code>을 진행한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/3db29906-f6bd-415c-bba4-8574f2f358f5/image.png" /></p>
<h4 id="4-배포하고자-하는-정적-파일을-업로드한다">4. 배포하고자 하는 정적 파일을 업로드한다.</h4>
<ul>
<li>아래와 같이 성공적으로 파일이 업로드된 것을 확인할 수 있다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/fcd6877e-9527-4e8f-9d9c-17fd7de0bf7e/image.png" /></p>
<h3 id="cloudfront-배포-설정하기">CloudFront 배포 설정하기</h3>
<h4 id="1-원본-도메인을-선택한다">1. 원본 도메인을 선택한다.</h4>
<ul>
<li><strong>Original domain</strong>: Origin을 지정하는 것으로, 앞에서 생성한 S3 버킷을 선택한다.</li>
<li><strong>Origin path</strong>: Origin에서 특정 경로의 객체만 불러올 것인지 전체를 불러올지를 결정할 수 있다. S3의 특정 폴더를 url로 지정하면 해당 폴더의 파일만 CloudFront에서 가져온다. 지정 여부는 선택 사항이다.</li>
<li><strong>이름</strong>: 해당 origin의 이름을 지정한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/54ac5d32-cb9e-4238-b88d-ce9ae0389803/image.png" /></li>
</ul>
<h4 id="2-s3-버킷의-액세스를-설정한다">2. S3 버킷의 액세스를 설정한다.</h4>
<ul>
<li>cloudFront가 데이터를 가져올 때 S3의 액세스 권한과 별개로 자체적인 권한을 부여할지 여부를 결정한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/814bd479-77b9-4f1d-8c91-0d4ebed56546/image.png" /></li>
</ul>
<h4 id="3-origin-shield를-활성화하고-원하는-region을-선택한다">3. Origin Shield를 활성화하고 원하는 Region을 선택한다.</h4>
<ul>
<li>지리적으로 가까운 Region을 선택하는 것이 좋다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/353ef50f-a333-4daf-937e-8cc2f19d2e3f/image.png" /></li>
</ul>
<blockquote>
<p><a href="https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html">Origin Shield</a>
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/26f4ef52-19ab-4345-a061-b418330a9b61/image.png" /></p>
</blockquote>
<ul>
<li>AWS CloudFront가 2020년에 발표한 중앙 집중식 캐싱 계층으로, 캐시 적중률을 높여 오리진의 부하를 줄이는 데 도움이 된다고 한다.</li>
<li>캐싱 계층을 하나 더 추가하여 사용자(클라이언트)와 엣지 서버 간의 거리를 줄여주는 것이다.</li>
<li>또한 여러 리전에 걸친 요청을 압축해 오리진으로 제출되는 객체당 요청을 최소 1개까지 줄임으로써 오리진 운영 비용을 절감해준다.</li>
<li>다만 Origin Shield를 활성화할 경우 요청이 Origin Shield를 경유할 때마다 요청 수수료가 발생된다.</li>
</ul>
<h4 id="4-추가-설정을-진행한다">4. 추가 설정을 진행한다.</h4>
<ul>
<li><strong>자동으로 객체 압축</strong>: <code>Yes</code>로 설정하면 요청할 리소스 파일 크기를 비약적으로 줄여준다.</li>
<li><strong>뷰어 프로토콜 정책</strong>: <code>Redirect HTTP to HTTPS</code>로 설정하면 <strong>HTTP</strong> 프로토콜로 접속할 경우 자동으로 <strong>HTTPS로 리다이렉트</strong> 된다.</li>
<li><strong>허용된 HTTP 방법</strong>: 정적 리소스를 배포하므로 다른 HTTP Method가 필요하지 않아 <code>GET, HEAD</code>로 설정하면 된다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/3e6f2394-de67-4e17-a6a9-cf8ffcf92dde/image.png" /></li>
</ul>
<h4 id="5-캐시-키-및-원본-요청을-설정한다">5. 캐시 키 및 원본 요청을 설정한다.</h4>
<ul>
<li>추가로 캐시 정책을 설정하지 않을 예정이었으므로 권장되는 캐시 정책이 적용되도록 하였다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/522f6fb5-8065-4f4c-b003-6b24d4b39e19/image.png" /></li>
</ul>
<h4 id="6--기본-값-루트-객체를-설정해준다">6.  기본 값 루트 객체를 설정해준다.</h4>
<ul>
<li>인덱스 페이지의 파일명을 입력하되 <code>/</code>를 입력하지 않도록 주의해야 한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/82c3cf01-dbbb-4137-a122-ec70ef6b9e08/image.png" /></li>
</ul>
<ul>
<li>필수적으로 설정해주어야 하는 것들은 기록해두었고, 기타 추가 설정의 경우 기본으로 두거나 필요에 따라 선택적으로 적용하면 된다.</li>
</ul>
<h3 id="cloudfront-오류-페이지-설정">CloudFront 오류 페이지 설정</h3>
<ul>
<li>React로 SPA 애플리케이션을 배포할 경우 Fallback Redirect 설정이 필요하다.</li>
<li><code>오류 페이지</code> 탭의 <code>사용자 정의 오류 응답 생성</code> 버튼을 클릭하여 설정할 수 있다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/fed5bab4-dfbd-420e-9b56-4d8ac9ca05fb/image.png" /></p>
<ul>
<li>S3에서는 찾는 파일이 없을 때 <code>403</code>을 응답하므로 HTTP 오류 코드를 <code>403</code>으로 설정한다.<ul>
<li>HTTP 오류 코드: <code>403</code></li>
<li>오류 응답 사용자 정의: <code>예</code></li>
<li>응답 페이지 경로: <code>/index.html</code></li>
<li>HTTP 응답 코드: <code>200</code></li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/f1f210b9-e251-455d-a0c5-77a54d7b9b25/image.png" /></p>
<ul>
<li>추가적으로 필요한 오류 페이지들을 설정해주면 된다.</li>
</ul>
<h3 id="s3-버킷-정책-업데이트">S3 버킷 정책 업데이트</h3>
<ul>
<li><p>CloudFront에서 S3에 접근하게 하기 위해서는 S3 정책을 업데이트 해주어야 한다.</p>
</li>
<li><p><code>정책 복사</code> 버튼을 클릭한 뒤 S3로 이동하여 버킷 정책을 업데이트 한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/44dc7c1e-8cac-41af-a8ea-47892f9e346b/image.png" /></p>
</li>
<li><p>S3의 <code>권한</code> 탭의 버킷 정책 부분에서 <code>편집</code> 버튼을 클릭한 뒤 앞에서 복사한 정책을 붙여 넣어준다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/dbc45519-4b5f-4fde-87cf-6f5a88a0df6e/image.png" /></p>
</li>
</ul>
<p>위의 과정을 거치면 배포된 도메인을 확인할 수 있게 된다✨</p>
<h1 id="github-actions를-활용하여-cicd-파이프라인-구축하기">Github Actions를 활용하여 CI/CD 파이프라인 구축하기</h1>
<h3 id="파일-빌드-전-기본-설정">파일 빌드 전 기본 설정</h3>
<blockquote>
<p><strong>checkout source code</strong></p>
</blockquote>
<p><code>actions/checkout</code> 액션을 사용하여 소스 코드를 체크아웃해 Github 레포지토리의 소스 코드를 작업 환경으로 가져온다.</p>
<pre><code class="language-yml">      - name: Checkout source code
        uses: actions/checkout@v3</code></pre>
<blockquote>
<p><strong>install pnpm</strong></p>
</blockquote>
<p><code>npm</code>을 사용하여 <code>pnpm</code>을 설치해준다. 여기서 설치된 <code>pnpm</code>은 이후 Node.js의 패키지 관리자로 사용된다.</p>
<pre><code class="language-yml">      - name: Install pnpm
        run: npm install pnpm -g</code></pre>
<blockquote>
<p><strong>install dependencies</strong></p>
</blockquote>
<p><code>pnpm</code>을 사용하여 프로젝트의 종속성을 설치해준다. 여기에서 프로젝트에 필요한 모든 패키지가 설치된다.</p>
<pre><code class="language-yml">      - name: Install dependencies
        run: pnpm install</code></pre>
<h3 id="파일-빌드하여-s3에-업로드하기">파일 빌드하여 S3에 업로드하기</h3>
<blockquote>
<p><strong>build</strong></p>
</blockquote>
<p>프로젝트를 빌드한다. Github Secrets에 환경 변수들을 설정하여 빌드 프로세스에 필요한 환경 변수를 제공한다.</p>
<pre><code class="language-yml">- name: build
        env:
          VITE_API_MOCKING: ${{secrets.VITE_API_MOCKING}}
          VITE_SERVER: ${{secrets.VITE_SERVER}}
          VITE_CRYPTO_KEY_NAME: ${{secrets.VITE_CRYPTO_KEY_NAME}}
          VITE_CRYPTO_KEY_LENGTH: ${{secrets.VITE_CRYPTO_KEY_LENGTH}}
        run: pnpm run build</code></pre>
<blockquote>
<p><strong>configure AWS credentials</strong></p>
</blockquote>
<p><a href="https://github.com/marketplace?type=">Github Marketplace</a>에 미리 구현되어 있는 <a href="https://github.com/marketplace/actions/configure-aws-credentials-action-for-github-actions">aws-actions/configure-aws-credentials</a>라는 action을 사용하여 AWS 자격 증명을 구성한다. 이를 통해 AWS의 서비스를 사용할 때 필요한 자격 증명을 설정할 수 있는데, 이 과정을 미리 진행하면 아래에서 사용할 다른 AWS 관련 액션들에서 별도의 인증을 진행하지 않아도 되어 편리하다. Github Secrets에서 가져온 환경변수들을 사용하여 구성한다.</p>
<pre><code class="language-yml">      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_S3_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_S3_SECRET_ACCESS_KEY_ID }}
          aws-region: ${{ secrets.AWS_REGION }}</code></pre>
<blockquote>
<p><strong>upload to s3</strong></p>
</blockquote>
<p>이 또한 Github Marketplace에 미리 구현된 <a href="https://github.com/jakejarvis/s3-sync-action">액션</a>을 사용해주었다. 이 액션을 통해 위의 작업을 통해 빌드된 프로젝트 파일을 AWS S3 버킷으로 업로드할 수 있다. 이 액션은 지정된 디렉토리(<code>SOURCE_DIR</code>)의 파일을 S3 버킷과 동기화하는데, 이때 파일의 ACL을 <code>public-read</code>로 설정하고, 이전에 업로드된 파일들을 삭제하게 된다. 업로드할 버킷 이름은 미리 Github Secrets에 환경 변수를 지정해주어야 한다. </p>
<pre><code class="language-yml">      - name: Upload to S3
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl public-read --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET_NAME}}
          SOURCE_DIR: 'dist'</code></pre>
<h3 id="aws-cloudfront-캐시-무효화하기">AWS CloudFront 캐시 무효화하기</h3>
<ul>
<li>S3에 있는 리소스를 새로 업로드하고 캐시를 무효화해야 할 때 cloudFront에서 캐시를 무효화한 뒤 새로운 캐시를 생성하도록 해주는 <a href="https://github.com/chetan/invalidate-cloudfront-action">액션</a>을 사용하였다.<pre><code class="language-yml">    - name: Invalidate CloudFront Cache
      uses: chetan/invalidate-cloudfront-action@master
      env:
        AWS_DISTRIBUTION: ${{ secrets.AWS_DISTRIBUTION_ID }}
        PATHS: '/index.html'
      # 작업 실행 중 에러가 발생해도 다음 단계를 실행하도록 설정한다.
      # 이렇게 설정하면 cloudFront 캐시 무효화 작업에서 에러가 발생해도 
      # workflow를 중단시키지 않는다.
      continue-on-error: true</code></pre>
</li>
</ul>
<h3 id="🚨-트러블-슈팅">🚨 트러블 슈팅</h3>
<ul>
<li><p>처음 jobs를 두 개로 나누어 구현했을 때 빌드 파일을 찾지 못해 S3에 빌드 파일을 업로드하는 부분에서 <code>The user-provided path ./build does not exist.</code> 에러가 발생하였다.</p>
<ul>
<li>경로를 지정해주면서 두 개의 jobs를 분리한 채로 유지하는 것과 ci/cd jobs를 하나로 합치는 것 중에서 고민하다가 하나로 합쳐도 작업 자체가 길지 않음에도 불필요하게 파일을 찾는 코드를 늘릴 필요는 없을 것 같아 하나의 jobs로 통합하였다.</li>
</ul>
</li>
<li><p>이후 동일한 부분에서 아래와 같은 다른 에러가 발생하였다. <strong><em>upload failed. ~ An Error occured (AccessControllistNotSupported) when calling the PutObject operation: The bucket does not allow ACLs.</em></strong></p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/13d3e010-bee8-4da8-bf4a-b2298075da5d/image.png" /></p>
<ul>
<li>이는 ACL이 비활성화 되어 있어 발생했던 문제로 아래와 같이 설정을 수정하여 해결하였다. 
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/455c5f86-a6db-4e8f-bcd0-6f6ef817121e/image.png" /></li>
</ul>
<blockquote>
<p>ACL</p>
</blockquote>
<ul>
<li>ACcess List</li>
<li>접근 제어 리스트를 통해 특정 주소를 가진 호스트의 접근을 막거나 특정 서비스를 차단하는 등의 필터링 기능을 사용할 수 있다.</li>
</ul>
<ul>
<li>추가로, 예상치 못한 부분에서 Action 에러가 발생한다면 github secret 변수와 workflow yml 파일에 작성한 <code>secrets.~</code>의 값이 동일한지 꼭 확인해보자..!</li>
</ul>
<h3 id="전체-github-actions-workflow는-아래와-같이-작성하였다">전체 Github Actions Workflow는 아래와 같이 작성하였다.</h3>
<pre><code class="language-yml">name: Admin-CICD

on:
  push:
    branches:
      - main

jobs:
  cicd:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v3

      - name: Install pnpm
        run: npm install pnpm -g

      - name: Install dependencies
        run: pnpm install

      - name: build
        env:
          VITE_API_MOCKING: ${{secrets.VITE_API_MOCKING}}
          VITE_SERVER: ${{secrets.VITE_SERVER}}
          VITE_CRYPTO_KEY_NAME: ${{secrets.VITE_CRYPTO_KEY_NAME}}
          VITE_CRYPTO_KEY_LENGTH: ${{secrets.VITE_CRYPTO_KEY_LENGTH}}
        run: pnpm run build

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_S3_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_S3_SECRET_ACCESS_KEY_ID }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Upload to S3
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl public-read --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET_NAME}}
          SOURCE_DIR: 'dist'

      - name: Invalidate CloudFront Cache
        uses: chetan/invalidate-cloudfront-action@master
        env:
          AWS_DISTRIBUTION: ${{ secrets.AWS_DISTRIBUTION_ID }}
          PATHS: '/index.html'
        continue-on-error: true</code></pre>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://aws.amazon.com/ko/blogs/korea/amazon-s3-amazon-cloudfront-a-match-made-in-the-cloud/">실전 Amazon S3와 CloudFront로 정적 파일 배포하기</a></li>
<li><a href="https://yozm.wishket.com/magazine/detail/1360/">AWS로 클라우드 시작하기:④S3 &amp;  CloudFront</a></li>
<li><a href="https://puterism.com/deploy-with-s3-and-cloudfront/">AWS S3 + CloudFront로 정적 웹 사이트 배포하기</a></li>
<li><a href="https://dev.classmethod.jp/articles/for-beginner-s3-explanation/">초보자도 이해할 수 있는 S3(Simple Storage Service)</a></li>
<li><a href="https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/Welcome.html">Amazon S3란 무엇인가요?</a></li>
<li><a href="https://aws.amazon.com/ko/compare/the-difference-between-block-file-object-storage/">블록, 객체, 파일 스토리지는 어떻게 다른가요?</a></li>
<li><a href="https://www.smileshark.kr/post/amazon-s3-efs-ebs-which-aws-storage-service-to-use">아마존 S3 vs EFS vs EBS : 어떤 AWS 스토리지를 써야 하나요?</a></li>
<li><a href="https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-CloudFront-%EA%B0%9C%EB%85%90-%EC%9B%90%EB%A6%AC-%EC%82%AC%EC%9A%A9-%EC%84%B8%ED%8C%85-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC">[AWS] 📚 CloudFront 개념 원리 &amp; 사용 세팅 💯 정리</a></li>
<li><a href="https://haon.blog/server/cloudfront-cdn/">AWS CloudFront로 CDN 환경 구축하기</a></li>
<li><a href="https://suvera.tistory.com/79">AWS ) 정적 웹 사이트 배포 방식 비교 ( nginx / cloudFront / amplify )</a></li>
</ul>