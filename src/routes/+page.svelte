<script lang="ts">
	import { tocCrawler } from '@skeletonlabs/skeleton';
	import Year from '$lib/component/history/year.svelte';
	import Item from '$lib/component/history/item.svelte';
</script>

<div class="container h-full mx-auto flex flex-col space-y-6 py-6" use:tocCrawler={{ mode: 'generate' }}>
	<Year year="2006">
		<Item summary="출생" />
	</Year>
	<hr />
	<Year year="2022">
		<Item summary="경기북과학고등학교 입학" />
	</Year>
	<hr />
	<Year year="2024">
		<Item summary="경기북과학고등학교 조기 졸업" />
		<hr />
		<Item summary="KAIST(한국과학기술원) 입학" />
		<Item summary="KAIST 학생문화공간위원회 합류" />
		<hr />
		<Item summary="KAIST 학생문화공간위원회 관리국장 승진" />
		<Item summary="Dean's List 수상">
			<svelte:fragment slot="content">
				<p class="h4">
					Dean's List 란?
				</p>
				<p>
					성적 취득을 기준으로 선정한 우등생. KAIST의 경우엔 해당 학기 상위 2% 이내에 든 학생 대상으로 수상하며, 새내기, 공과대학, 자연대학 등을 나눠서 수상함
				</p>
				<p>
					24년도 가을학기에 <strong>평점 4.12</strong>를 취득하며, 새내기 Dean's List 상을 수상함
				</p>
			</svelte:fragment>
		</Item>
	</Year>
	<Year year="2025">
		<Item summary="전산학부 진입" />
		<Item summary="전산학부 집행위원회 합류" />
	</Year>
</div>

<style lang="postcss">
    /*figure {*/
    /*    @apply flex relative flex-col;*/
    /*} 2022 1학년 */

    /*figure svg,*/
    /*.img-bg {*/
    /*    @apply w-64 h-64 md:w-80 md:h-80;*/
    /*}*/

    /*.img-bg {*/
    /*    @apply absolute z-[-1] rounded-full blur-[50px] transition-all;*/
    /*    animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,*/
    /*    glow 5s linear infinite;*/
    /*}*/

    @keyframes glow {
        0% {
            @apply bg-primary-400/50;
        }
        33% {
            @apply bg-secondary-400/50;
        }
        66% {
            @apply bg-tertiary-400/50;
        }
        100% {
            @apply bg-primary-400/50;
        }
    }

    @keyframes pulse {
        50% {
            transform: scale(1.5);
        }
    }
</style>
