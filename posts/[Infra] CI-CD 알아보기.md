<h2 id="♾️-cicd란">♾️ CI/CD란?</h2>
<img src="https://velog.velcdn.com/images/hamjw0122/post/8f2b2218-6dec-452c-9fea-af3cc71212d5/image.png" width="50%" />

<ul>
<li>어플리케이션 개발 단계에서부터 배포 때까지의 모든 단계들을 자동화를 통해 더 효율적이고 빠르게 사용자에게 빈번이 배포할 수 있도록 만드는 것</li>
<li>애플리케이션의 빌드, 테스트, 패키지화, 배포 단계를 모두 자동화해주며 그 과정에서 생성한 컨테이너는 로컬 개발 환경과 운영 개발 환경 모두에 배포하고 실행할 수 있다.</li>
</ul>
<h3 id="⛓️-cicd-파이프라인">⛓️ CI/CD 파이프라인</h3>
<ol>
<li>개발자는 작은 단위로 기능을 나누어 주기적으로 메인 레포지토리에 코드를 머지한다.</li>
<li>자동으로 빌드, 테스트 과정을 실행하며 릴리즈를 준비한다.</li>
<li>자동/수동으로 릴리즈 버전을 최종 배포한다.</li>
</ol>
<h3 id="🛠️-cicd-구현을-위한-툴">🛠️ CI/CD 구현을 위한 툴</h3>
<ul>
<li>Jenkins</li>
<li>Buildkit</li>
<li>GitHub Actions</li>
<li>GitLab CI/CD</li>
<li>Bitbucket Pipelines</li>
<li>circleci</li>
</ul>
<h2 id="🌟-ci-톺아보기">🌟 CI 톺아보기</h2>
<h3 id="📍-ci-개요">📍 CI 개요</h3>
<blockquote>
<p><strong><em>Continuous Integration</em></strong>
: 지속적인 통합</p>
</blockquote>
<ul>
<li><p>지속적으로 개발자의 작업물(코드)이 완성된 상태의 서비스가 되도록 머지하는 프로세스</p>
</li>
<li><p>자동화된 빌드 및 테스트가 수행된 후 개발자가 코드 변경 사항을 중앙 레포지토리에 정기적으로 병합하는 데브옵스 소프트웨어 개발 방식</p>
</li>
<li><p>애플리케이션의 새로운 코드 변경 사항이 정기적으로 빌드 및 테스트되어 공유 레포지토리에 통합되는 것</p>
</li>
<li><p>주로 소프트웨어 릴리즈 과정 중 빌드 또는 통합 단계를 가리킨다.</p>
</li>
<li><p>개발자들은 코드 변경 사항을 <strong>주기적으로 빈번하게</strong> 머지해야 한다.</p>
</li>
<li><p>통합을 위한 단계(빌드, 테스트, 머지)의 <strong>자동화</strong></p>
<ol>
<li>주기적으로 메인 레포지토리에 코드 변경 사항을 머지한다. (with 코드 리뷰)</li>
<li>자동으로 팀에서 만든 CI 스크립트를 통해 추가된 코드와 함께 레포지토리가 빌드된다.</li>
<li>성공적으로 빌드 되었을 경우 팀에서 작성한 테스트들이 스크립트를 통해 실행된다.</li>
<li>성공 시 배포할 때 무사히 반영된다. </li>
<li>하지만 새로 추가된 코드에 문제가 있어 빌드가 실패하거나 테스트에서 성공한다면 Red Sign이 뜨며 자동으로 문제 원인을 일으킨 개발자에게 알려준다.</li>
</ol>
</li>
<li><p>자동화 구성 요소(CI, 빌드 서비스), 문화적 구성 요소(빈번하게 통합하도록 학습하기)를 모두 포함한다.</p>
</li>
</ul>
<h3 id="✨-ci의-장점">✨ CI의 장점</h3>
<ul>
<li>버그를 찾아 신속하게 해결하고, 소프트웨어 품질을 개선하고 새로운 소프트웨어 업데이트를 검증 및 릴리즈하는 데 걸리는 시간을 단축할 수 있다.</li>
<li>주기적으로 머지하기 때문에 충돌을 피할 수 있어 개발 생산성을 향상시킬 수 있다.</li>
<li>머지되는 모든 코드들이 자동으로 빌드되고 테스트되므로 코드의 결함이나 문제점을 빠르게 발견할 수 있다.</li>
<li>주기적인 머지 덕분에 코드의 변경 사항이 작기 때문에 발견된 버그들이 조금 더 고립되고 작은 단위가 되므로 빠르게 수정할 수 있다.</li>
</ul>
<p>➡️ 코드의 퀄리티를 향상시킬 수 있다.</p>
<h2 id="🌟-cd-톺아보기">🌟 CD 톺아보기</h2>
<h3 id="📍-cd-개요">📍 CD 개요</h3>
<blockquote>
<p><strong><em>Continuous Delivery/Deployment</em></strong>
: 지속적인 제공</p>
</blockquote>
<ul>
<li>짧은 주기로 소프트웨어를 개발하는 소프트웨어 공학적 접근의 하나</li>
<li>프로덕션에 릴리즈하기 위한 코드 변경이 자동으로 준비되는 소프트웨어 개발 방식</li>
<li>개발자들이 애플리케이션에 적용한 변경 사항이 버그 테스트를 거쳐 레포지토리에 자동으로 업로드 되는 것</li>
<li>빌드 단계 이후의 모든 코드 변경을 테스트 환경 및(또는) 프로덕션 환경에 배포하여 지속적 통합을 확장한다.</li>
</ul>
<blockquote>
<p>지속적 제공에서의 CD(<strong><em>Delivery</em></strong>)</p>
</blockquote>
<ul>
<li>애플리케이션에 적용한 코드의 빌드와 테스트를 성공적으로 진행했을 때 깃허브와 같은 코드 저장소에 자동으로 업로드하는 과정</li>
<li>최소의 노력으로 코드 배포를 쉽게 하도록 해준다.</li>
</ul>
<blockquote>
<p>지속적 배포에서의 CD(<strong><em>Deployment</em></strong>)</p>
</blockquote>
<ul>
<li>지속적 제공을 통해 성공적으로 병합한 코드 내역을 AWS와 같은 배포 환경으로 보내는 것 (= <strong>릴리즈</strong>)</li>
<li>지속적 제공의 다음 단계까지 자동화한다.<ul>
<li>개발자가 애플리케이션에 변경 사항을 커밋하면 몇 분 이내에 애플리케이션을 자동으로 배포하여 적용시킨다.</li>
</ul>
</li>
</ul>
<h3 id="✨-cd의-장점">✨ CD의 장점</h3>
<ul>
<li>소프트웨어가 언제든지 신뢰 가능한 수준으로 출시될 수 있도록 보증 할 수 있다.</li>
<li>소프트웨어를 더 주기적이고 빠르게 빌드하고 테스트하고 출시할 수 있다.</li>
<li>적절하게 구현될 경우 언제나 즉시 배포 가능하고 표준화된 테스트 프로세스를 통과한 빌드 아티팩트(산출물)를 보유할 수 있다.</li>
<li>다양한 테스트를 자동화하여 고객에게 배포되기 전 여러 차원에서 애플리케이션 업데이트를 확인할 수 있다.</li>
<li>업데이트를 좀 더 철저히 검증하고 문제를 사전에 발견할 수 있다.</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://www.youtube.com/watch?v=0Emq5FypiMM">CI/CD 5분 개념 정리 (현업에서 쓰는 개발 프로세스)</a></li>
<li><a href="https://engineering.linecorp.com/ko/blog/ci-cd-automation?ref=codenary">CI/CD 자동화가 가져다 준 행복</a></li>
<li><a href="https://mesh.dev/20210208-dev-notes-002-ci-cd/?ref=codenary">CI/CD 도구 및 방법론 도입기</a></li>
<li><a href="https://devinn.dev/blog/detail/253?ref=codenary">지속적 통합과 배포 자동화를 위한 CI/CD 툴</a></li>
<li><a href="https://techblog.woowahan.com/2579/?ref=codenary">라이더스 개발팀 모바일에서 CI/CD 도입</a></li>
<li><a href="https://www.samsungsds.com/kr/insights/intelligent_automation_in_ci_cd.html?ref=codenary">지능형 자동화, 성공적인 CI/CD를 위한 핵심</a></li>
<li><a href="https://yozm.wishket.com/magazine/detail/2184/">CI/CD 개념과 깃허브 리포지터리 생성하기</a></li>
</ul>