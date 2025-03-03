<script lang="ts">
	import { tocCrawler } from '@skeletonlabs/skeleton';
	import Year from '$lib/component/history/year.svelte';
	import Month from '$lib/component/history/month.svelte';
	import Item from '$lib/component/history/item.svelte';

	let tabIndex = 0;
</script>

<div class="h-full w-full px-12 flex flex-col space-y-6 py-6" use:tocCrawler={{ mode: 'generate', key: tabIndex }}>
	<Year year="2006">
		<Month month="07">
			<Item summary="출생" />
		</Month>
	</Year>
	<hr class="w-full" />
	<Year year="2022">
		<Month month="02">
			<Item summary="경기북과학고등학교 입학" />
		</Month>
	</Year>
	<hr />
	<Year year="2024">
		<Month month="01">
			<Item summary="경기북과학고등학교 조기 졸업" />
		</Month>
		<hr />
		<Month month="02">
			<Item summary="KAIST 입학" />
			<Item summary="KAIST 학생문화공간위원회 입회 (관리국 개발팀)" />
		</Month>
		<hr />
		<Month month="09">
			<Item summary="KAIST 학생문화공간위원회 관리국장 승진" />
		</Month>
	</Year>
	<Year year="2025">
		<Month month="02">
			<Item summary="전산학부 진입" />
			<Item summary="전산학부 집행위원회 입회 (비서실)" />
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
		</Month>
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
