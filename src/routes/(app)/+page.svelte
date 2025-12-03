<script lang="ts">
	import { onMount } from 'svelte';

	const discordSrc = 'https://discord.gg/aulazero';
	const githubSrc = 'https://github.com/skeletonlabs/skeleton'; // Mantendo o link original, mas talvez devesse ser o do projeto

	let scrollY = $state(0);
	let innerHeight = $state(0);
	let innerWidth = $state(0);

	let horizontalSection: HTMLElement | undefined = $state();
	let horizontalTrack: HTMLElement | undefined = $state();

	onMount(() => {
		const observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					entry.target.classList.add('show');
				}
			});
		});

		const hiddenElements = document.querySelectorAll('.hidden-scroll');
		hiddenElements.forEach((el) => observer.observe(el));
	});

	// Horizontal Scroll Logic
	$effect(() => {
		// Access scrollY to ensure reactivity
		const _ = scrollY;
		
		if (horizontalSection && horizontalTrack && innerWidth > 768) {
			const rect = horizontalSection.getBoundingClientRect();
			const sectionTop = rect.top; // Posição do topo da seção em relação ao viewport
			const sectionHeight = rect.height;
			const windowHeight = innerHeight;
			
			// O quanto já rolamos DENTRO da seção (considerando que ela começa no topo da tela)
			// Como ela é sticky, o "topo" visual fica fixo, mas o rect.top continua diminuindo (ficando negativo)
			const scrollDistance = -sectionTop;
			const maxScroll = sectionHeight - windowHeight;

			if (scrollDistance >= 0 && scrollDistance <= maxScroll) {
				const progress = scrollDistance / maxScroll;
				const trackWidth = horizontalTrack.scrollWidth;
				const moveAmount = trackWidth - innerWidth;
				horizontalTrack.style.transform = `translateX(-${progress * moveAmount}px)`;
			} else if (scrollDistance < 0) {
				horizontalTrack.style.transform = `translateX(0px)`;
			} else if (scrollDistance > maxScroll) {
				const trackWidth = horizontalTrack.scrollWidth;
				const moveAmount = trackWidth - innerWidth;
				horizontalTrack.style.transform = `translateX(-${moveAmount}px)`;
			}
		}
	});
</script>

<svelte:window bind:scrollY bind:innerHeight bind:innerWidth />

<svelte:head>
	<title>Legacy - Aula Zero</title>
	<meta
		name="description"
		content="Aprenda matemática, pague o que quiser - Aula Zero, o aluno em primeiro lugar!"
	/>
</svelte:head>

<!-- Navbar Fixa -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top shadow-sm transition-all" class:scrolled={scrollY > 50}>
	<div class="container">
		<a class="navbar-brand fw-bold d-inline-flex align-items-center" href="/">
			<img src="https://raw.githubusercontent.com/AulaZero/icons/refs/heads/main/icons/azr-white-bg-transparent.svg" alt="Logo" width="30" height="30" class="d-inline-block align-text-top me-2">
			<span>Legacy</span>
		</a>
		<div class="d-flex gap-4">
			<a href={githubSrc} target="_blank" class="text-white" title="GitHub">
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-github" viewBox="0 0 16 16">
					<path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"/>
				</svg>
			</a>
			<a href={discordSrc} target="_blank" class="text-white" title="Discord">
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-discord" viewBox="0 0 16 16">
					<path d="M13.545 2.907a13.227 13.227 0 0 0-3.257-1.011.05.05 0 0 0-.052.025c-.141.25-.297.577-.406.833a12.19 12.19 0 0 0-3.658 0 8.258 8.258 0 0 0-.412-.833.051.051 0 0 0-.052-.025c-1.125.194-2.22.534-3.257 1.011a.041.041 0 0 0-.021.018C.356 6.024-.213 9.047.066 12.032c.001.014.01.028.021.037a13.276 13.276 0 0 0 3.995 2.02.05.05 0 0 0 .056-.019c.308-.42.582-.863.818-1.329a.05.05 0 0 0-.01-.059.051.051 0 0 0-.018-.011 8.875 8.875 0 0 1-1.248-.595.05.05 0 0 1-.02-.066.051.051 0 0 1 .015-.019c.084-.063.168-.129.248-.195a.05.05 0 0 1 .051-.007c2.619 1.196 5.454 1.196 8.041 0a.052.052 0 0 1 .053.007c.08.066.164.132.248.195a.051.051 0 0 1-.004.085 8.254 8.254 0 0 1-1.249.594.05.05 0 0 0-.03.03.052.052 0 0 0 .003.041c.24.465.515.909.817 1.329a.05.05 0 0 0 .056.019 13.235 13.235 0 0 0 4.001-2.02.049.049 0 0 0 .021-.037c.334-3.451-.559-6.449-2.366-9.106a.034.034 0 0 0-.02-.019Zm-8.198 7.307c-.789 0-1.438-.724-1.438-1.612 0-.889.637-1.613 1.438-1.613.807 0 1.45.73 1.438 1.613 0 .888-.637 1.612-1.438 1.612Zm5.316 0c-.788 0-1.438-.724-1.438-1.612 0-.889.637-1.613 1.438-1.613.807 0 1.451.73 1.438 1.613 0 .888-.631 1.612-1.438 1.612Z"/>
				</svg>
			</a>
		</div>
	</div>
</nav>

<!-- Hero Section -->
<header class="hero-section d-flex align-items-center justify-content-center text-center text-white position-relative overflow-hidden">
	<div class="hero-bg"></div>
	<div class="container position-relative z-2 hidden-scroll">
		<h1 class="display-1 fw-bold mb-4 text-shadow">Aula Zero Legacy</h1>
		<p class="lead mb-5 fs-3 text-shadow-sm">Para encerrar seus problemas com matemática</p>
		<a href="./game" class="btn btn-light btn-lg px-5 py-3 rounded-pill fw-bold shadow-lg hover-scale">
			Começar Agora
		</a>
	</div>
	<div class="scroll-down-indicator">
		<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="currentColor" class="bi bi-chevron-down animate-bounce" viewBox="0 0 16 16">
			<path fill-rule="evenodd" d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z"/>
		</svg>
	</div>
</header>

<!-- Seção de Recursos -->
<section class="py-5 bg-light">
	<div class="container py-5">
		<div class="row justify-content-center mb-5 hidden-scroll">
			<div class="col-lg-8 text-center">
				<h2 class="fw-bold mb-3">Aprenda de forma significativa</h2>
				<p class="text-muted fs-5">O essencial da matemática de forma simples, interativa e direta ao ponto.</p>
			</div>
		</div>

		<div class="row g-4">
			<div class="col-md-4 hidden-scroll delay-100">
				<div class="card h-100 border-0 shadow-sm hover-card">
					<div class="card-body text-center p-4">
						<div class="icon-box mb-3 text-primary-500 d-inline-block">
							<svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" fill="currentColor" class="bi bi-controller" viewBox="0 0 16 16">
								<path d="M11.5 6.027a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0m-1.5 1.5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1m2.5-.5a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0m-1.5 1.5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1m-6.5-3h1v1h1v1h-1v1h-1v-1h-1v-1h1z"/>
								<path d="M3.051 3.26a.5.5 0 0 1 .354-.613l1.932-.518a.5.5 0 0 1 .62.39c.655-.079 1.35-.117 2.043-.117.72 0 1.443.041 2.12.126a.5.5 0 0 1 .622-.399l1.932.518a.5.5 0 0 1 .306.729q.211.136.373.297c.408.408.78 1.05 1.095 1.772.32.733.599 1.591.805 2.466s.34 1.78.364 2.606c.024.816-.059 1.602-.328 2.21a1.42 1.42 0 0 1-1.445.83c-.636-.067-1.115-.394-1.513-.773-.245-.232-.496-.526-.739-.808-.126-.148-.25-.292-.368-.423-.728-.804-1.597-1.527-3.224-1.527s-2.496.723-3.224 1.527c-.119.131-.242.275-.368.423-.243.282-.494.575-.739.808-.398.38-.877.706-1.513.773a1.42 1.42 0 0 1-1.445-.83c-.27-.608-.352-1.395-.329-2.21.024-.826.16-1.73.365-2.606.206-.875.486-1.733.805-2.466.315-.722.687-1.364 1.094-1.772a2.3 2.3 0 0 1 .433-.335l-.028-.079zm2.036.412c-.877.185-1.469.443-1.733.708-.276.276-.587.783-.885 1.465a14 14 0 0 0-.748 2.295 12.4 12.4 0 0 0-.339 2.406c-.022.755.062 1.368.243 1.776a.42.42 0 0 0 .426.24c.327-.034.61-.199.929-.502.212-.202.4-.423.615-.674.133-.156.276-.323.44-.504C4.861 9.969 5.978 9.027 8 9.027s3.139.942 3.965 1.855c.164.181.307.348.44.504.214.251.403.472.615.674.318.303.601.468.929.503a.42.42 0 0 0 .426-.241c.18-.408.265-1.02.243-1.776a12.4 12.4 0 0 0-.339-2.406 14 14 0 0 0-.748-2.295c-.298-.682-.61-1.19-.885-1.465-.264-.265-.856-.523-1.733-.708-.85-.179-1.877-.27-2.913-.27s-2.063.091-2.913.27"/>
							</svg>
						</div>
						<h5 class="card-title fw-bold">Gamificação</h5>
						<p class="card-text">Aprenda jogando. Avance passo a passo, um conceito de cada vez, como em um jogo.</p>
					</div>
				</div>
			</div>
			<div class="col-md-4 hidden-scroll delay-200">
				<div class="card h-100 border-0 shadow-sm hover-card">
					<div class="card-body text-center p-4">
						<div class="icon-box mb-3 text-primary-500 d-inline-block">
							<svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" fill="currentColor" class="bi bi-clipboard2-data" viewBox="0 0 16 16">
								<path d="M9.5 0a.5.5 0 0 1 .5.5.5.5 0 0 0 .5.5.5.5 0 0 1 .5.5V2a.5.5 0 0 1-.5.5h-5A.5.5 0 0 1 5 2v-.5a.5.5 0 0 1 .5-.5.5.5 0 0 0 .5-.5.5.5 0 0 1 .5-.5z"/>
								<path d="M3 2.5a.5.5 0 0 1 .5-.5H4a.5.5 0 0 0 0-1h-.5A1.5 1.5 0 0 0 2 2.5v12A1.5 1.5 0 0 0 3.5 16h9a1.5 1.5 0 0 0 1.5-1.5v-12A1.5 1.5 0 0 0 12.5 1H12a.5.5 0 0 0 0 1h.5a.5.5 0 0 1 .5.5v12a.5.5 0 0 1-.5.5h-9a.5.5 0 0 1-.5-.5z"/>
								<path d="M10 7a1 1 0 1 1 2 0v5a1 1 0 1 1-2 0zm-6 4a1 1 0 1 1 2 0v1a1 1 0 1 1-2 0zm4-3a1 1 0 0 0-1 1v3a1 1 0 1 0 2 0V9a1 1 0 0 0-1-1"/>
							</svg>
						</div>
						<h5 class="card-title fw-bold">Progresso Real</h5>
						<p class="card-text">Visualize sua evolução e domine a matemática do zero ao avançado.</p>
					</div>
				</div>
			</div>
			<div class="col-md-4 hidden-scroll delay-300">
				<div class="card h-100 border-0 shadow-sm hover-card">
					<div class="card-body text-center p-4">
						<div class="icon-box mb-3 text-primary-500 d-inline-block">
							<svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" fill="currentColor" class="bi bi-lightbulb" viewBox="0 0 16 16">
								<path d="M2 6a6 6 0 1 1 10.174 4.31c-.203.196-.359.4-.453.619l-.762 1.769A.5.5 0 0 1 10.5 13a.5.5 0 0 1 0 1 .5.5 0 0 1 0 1l-.224.447a1 1 0 0 1-.894.553H6.618a1 1 0 0 1-.894-.553L5.5 15a.5.5 0 0 1 0-1 .5.5 0 0 1 0-1 .5.5 0 0 1-.46-.302l-.761-1.77a2 2 0 0 0-.453-.618A5.98 5.98 0 0 1 2 6m6-5a5 5 0 0 0-3.479 8.592c.263.254.514.564.676.941L5.83 12h4.342l.632-1.467c.162-.377.413-.687.676-.941A5 5 0 0 0 8 1"/>
							</svg>
						</div>
						<h5 class="card-title fw-bold">Open Source</h5>
						<p class="card-text">Projeto de código aberto, gratuito e acessível para todos. Educação sem barreiras.</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Rolagem Horizontal -->
<section class="horizontal-scroll-section" bind:this={horizontalSection}>
	<div class="sticky-wrapper">
		<div class="container-fluid h-100 d-flex align-items-center">
			<div class="horizontal-track d-flex align-items-center gap-5 px-5" bind:this={horizontalTrack}>
				
				<!-- Card de Introdução -->
				<div class="scroll-item bg-primary-500 text-white p-5 rounded-4 shadow-lg d-flex flex-column justify-content-center">
					<h2 class="display-4 fw-bold mb-3">Sua Jornada</h2>
					<p class="fs-4">O caminho para a maestria matemática começa aqui.</p>
					<div class="mt-auto">
						<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
							<path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
						</svg>
					</div>
				</div>

				<!-- Nível 1 -->
				<div class="scroll-item bg-white p-5 rounded-4 shadow-sm border d-flex flex-column">
					<span class="badge bg-primary w-auto align-self-start mb-3">Fase 1</span>
					<h3 class="fw-bold mb-3">Fundamentos</h3>
					<p class="text-muted mb-4">Domine as operações básicas e a lógica inicial. Sem uma base sólida, não há construção.</p>
					<div class="mt-auto bg-light rounded d-flex align-items-center justify-content-center" style="height: 200px;">
						<span class="text-muted fw-bold fs-1">1 + 1 = 2</span>
					</div>
				</div>

				<!-- Nível 2 -->
				<div class="scroll-item bg-white p-5 rounded-4 shadow-sm border d-flex flex-column">
					<span class="badge bg-success w-auto align-self-start mb-3">Fase 2</span>
					<h3 class="fw-bold mb-3">Álgebra</h3>
					<p class="text-muted mb-4">Entenda as variáveis e equações. O mundo começa a ser descrito por letras e números.</p>
					<div class="mt-auto bg-light rounded d-flex align-items-center justify-content-center" style="height: 200px;">
						<span class="text-muted fw-bold fs-1">x² + y²</span>
					</div>
				</div>

				<!-- Nível 3 -->
				<div class="scroll-item bg-white p-5 rounded-4 shadow-sm border d-flex flex-column">
					<span class="badge bg-warning text-dark w-auto align-self-start mb-3">Fase 3</span>
					<h3 class="fw-bold mb-3">Geometria</h3>
					<p class="text-muted mb-4">Visualize o espaço e as formas. A matemática ganha corpo e dimensão.</p>
					<div class="mt-auto bg-light rounded d-flex align-items-center justify-content-center" style="height: 200px;">
						<svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" fill="currentColor" class="bi bi-box text-muted" viewBox="0 0 16 16">
							<path d="M8.186 1.113a.5.5 0 0 0-.372 0L1.846 3.5 8 5.961 14.154 3.5 8.186 1.113zM15 4.239l-6.5 2.6v7.922l6.5-2.6V4.24zM7.5 14.762V6.838L1 4.239v7.923l6.5 2.6zM7.443.184a1.5 1.5 0 0 1 1.114 0l7.129 2.852A.5.5 0 0 1 16 3.5v8.662a1 1 0 0 1-.629.928l-7.185 2.874a.5.5 0 0 1-.372 0L.63 13.09a1 1 0 0 1-.63-.928V3.5a.5.5 0 0 1 .314-.464L7.443.184z"/>
						</svg>
					</div>
				</div>

				<!-- Nível 4 -->
				<div class="scroll-item bg-white p-5 rounded-4 shadow-sm border d-flex flex-column">
					<span class="badge bg-danger w-auto align-self-start mb-3">Fase 4</span>
					<h3 class="fw-bold mb-3">Cálculo</h3>
					<p class="text-muted mb-4">O estudo da mudança. Limites, derivadas e integrais para entender o movimento.</p>
					<div class="mt-auto bg-light rounded d-flex align-items-center justify-content-center" style="height: 200px;">
						<span class="text-muted fw-bold fs-1">∫ f(x) dx</span>
					</div>
				</div>

				<!-- Card Final -->
				<div class="scroll-item bg-dark text-white p-5 rounded-4 shadow-lg d-flex flex-column justify-content-center text-center">
					<h2 class="fw-bold mb-4">Pronto para começar?</h2>
					<a href="./game" class="btn btn-light btn-lg rounded-pill fw-bold px-5 hover-scale ">Jogar Agora</a>
				</div>

			</div>
		</div>
	</div>
</section>

<!-- Seção de Doação -->
<section class="py-5 bg-dark text-white position-relative overflow-hidden">
	<div class="container py-5 hidden-scroll">
		<div class="row align-items-center">
			<div class="col-lg-6 mb-5 mb-lg-0">
				<h2 class="display-5 fw-bold mb-4">Apoie o Projeto</h2>
				<p class="lead mb-4">
					O Legacy é mantido pela comunidade e por doações. Seu apoio nos ajuda a manter os servidores online e desenvolver novas funcionalidades.
				</p>
				<div class="d-flex align-items-center gap-3 mb-4">
					<img src="https://raw.githubusercontent.com/AulaZero/icons/refs/heads/main/icons/azr-white-bg-transparent.svg" alt="Aula Zero" height="60">
					<div class="mx-1 d-flex align-items-center" aria-hidden="true">
						<div style="width:3px; height:48px;  background: white; border-radius:4px; box-shadow:0 2px 6px rgba(0,0,0,0.25);"></div>
					</div>
					<span class="fs-5">O aluno em <strong class="">primeiro lugar</strong>。</span>
				</div>
			</div>
			<div class="col-lg-6">
				<div class="card bg-white text-dark border-0 shadow-lg rounded-4 overflow-hidden">
					<div class="card-body p-0 d-flex flex-column flex-md-row">
						<div class="p-4 flex-grow-1 d-flex flex-col items-center justify-center text-center">
							<h5 class="fw-bold mb-3">Faça um Pix</h5>
							<img src="qrcode.png" alt="QR Code Pix" class="img-fluid mb-3 rounded border" style="max-width: 180px;">
							<p class="small text-muted mb-0">Chave: 49.079.681/0001-14</p>
							<p class="small text-muted">Nome: AULA ZERO</p>
						</div>
						<div class="bg-light p-4 d-flex flex-column justify-content-center align-items-center border-start-md">
							<img src="inter-logo.png" alt="Inter" height="30" class="mb-2">
							<span class="badge bg-secondary">Conta PJ</span>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<footer class="bg-black text-white-50 py-4 text-center">
	<div class="container">
		<small>&copy; {new Date().getFullYear()} Aula Zero. Todos os direitos reservados.</small>
	</div>
</footer>

<style>
	/* Fundo do Hero com Animação de Gradiente */
	.hero-section {
		height: 100vh;
		background: linear-gradient(-45deg, #0f0c29, #302b63, #24243e);
		background-size: 400% 400%;
		animation: gradientBG 15s ease infinite;
	}

	@keyframes gradientBG {
		0% { background-position: 0% 50%; }
		50% { background-position: 100% 50%; }
		100% { background-position: 0% 50%; }
	}

	.hero-bg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
		opacity: 0.3;
	}

	.text-shadow {
		text-shadow: 0 4px 10px rgba(0,0,0,0.5);
	}
	
	.text-shadow-sm {
		text-shadow: 0 2px 5px rgba(0,0,0,0.3);
	}

	/* Scroll Animations */
	.hidden-scroll {
		opacity: 1; /* Começar visível */
		transform: translateY(30px);
		transition: all 1s ease-out;
	}

	:global(.show) {
		opacity: 1;
		transform: translateY(0);
	}

	.delay-100 { transition-delay: 100ms; }
	.delay-200 { transition-delay: 200ms; }
	.delay-300 { transition-delay: 300ms; }

	/* Hover Effects */
	.hover-scale {
		transition: transform 0.3s ease;
	}
	.hover-scale:hover {
		transform: scale(1.05);
	}

	.hover-card {
		transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.2s ease;
		border: 2px solid transparent; /* allow border to appear on hover */
		border-radius: 0.5rem; /* match rounded corners */
	}
	.hover-card:hover {
		transform: translateY(-10px);
		box-shadow: 0 1rem 3rem rgba(0,0,0,.175)!important;
		border-color: var(--bs-primary) !important; /* use bootstrap primary */
	}
	.hover-card:focus-visible,
	.hover-card:focus-within {
		border-color: var(--bs-primary) !important;
		box-shadow: 0 0 0 0.25rem rgba(13,110,253,0.12) !important; /* small focus ring */
		outline: none !important;
	}

	.icon-box {
		transition: transform 0.3s ease;
		display: inline-block; /* prevents growing to one side */
		transform-origin: center center; /* scale from center */
		vertical-align: middle;
	}
	.hover-card:hover .icon-box {
		transform: scale(1.2);
	}

	/* Scroll Down Indicator */
	.scroll-down-indicator {
		position: absolute;
		bottom: 30px;
		left: 50%;
		transform: translateX(-50%);
		color: rgba(255,255,255,0.7);
	}

	.animate-bounce {
		animation: bounce 2s infinite;
	}

	@keyframes bounce {
		0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
		40% { transform: translateY(-10px); }
		60% { transform: translateY(-5px); }
	}

	/* Navbar Transition */
	.navbar {
		transition: background-color 0.3s ease, padding 0.3s ease;
	}
	.navbar:not(.scrolled) {
		background-color: transparent !important;
		padding-top: 1.5rem;
		padding-bottom: 1.5rem;
		box-shadow: none !important;
	}

	/* Horizontal Scroll Section */
	.horizontal-scroll-section {
		height: 400vh; /* Controla a duração do scroll */
		position: relative;
	}

	.sticky-wrapper {
		position: sticky;
		top: 0;
		height: 100vh;
		overflow: hidden;
		background-color: #f8f9fa;
	}

	.horizontal-track {
		width: max-content;
		will-change: transform;
	}

	.scroll-item {
		width: 400px;
		height: 500px;
		flex-shrink: 0;
		transition: transform 0.3s ease;
	}

	.scroll-item:hover {
		transform: translateY(-10px);
	}
</style>
