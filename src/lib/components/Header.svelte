<script>
	import { page } from '$app/state';
	import { base } from '$app/paths';
	import ThemeSwitcher from './ThemeSwitcher.svelte';
	import LanguageSwitcher from './LanguageSwitcher.svelte';
	import { t } from '$lib/i18n/store';

	// Menu items now use translation keys
	const menuItems = [
		{ titleKey: 'header.about', path: '/' },
		{ titleKey: 'header.news', path: '/about' },
		{ titleKey: 'header.contribute', path: '/contribute' },
		{ titleKey: 'header.contact', path: '/contact' },
		
	];

	let mobileMenuOpen = false;

	function toggleMobileMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}
	function closeMobileMenu() {
		mobileMenuOpen = false;
	}
</script>

<header class="site-header">
	<div class="header-content">
		<div class="navbar navbar-expand-lg fixed-top bg-primary" data-bs-theme="dark">
			<div class="container">
				<a href="../" class="navbar-brand" on:click={closeMobileMenu}>
					mRemoteNG
				</a>
				<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="true" aria-label="Toggle navigation">
					<span class="navbar-toggler-icon"></span>
				</button>
				
				<div class="navbar-collapse collapse show" id="navbarResponsive">
					<!-- Left side of the navbar -->
					<ul class="navbar-nav">
						{#each menuItems as item}
							<li class='nav-item' data-bs-theme="light">
								<a class="nav-link" href="{base}{item.path}">
									{$t(item.titleKey)}
								</a>
							</li>
						{/each}
					</ul>
					<!-- Right side of the navbar -->
					<ul class="navbar-nav ms-md-auto">
						<li class="nav-item">
							<a target="_blank" rel="noopener" class="nav-link" href="/downloads">
								<i class="bi bi-download"></i><span class="d-lg-none ms-2">{$t('header.downloads')}</span>
							</a>
						</li>
						<li class="nav-item">
							<a target="_blank" rel="noopener" class="nav-link" href="https://github.com/mRemoteNG/mRemoteNG">
								<i class="bi bi-github"></i><span class="d-lg-none ms-2">{$t('header.github')}</span>
							</a>
						</li>
						<li class="nav-item">
							<a target="_blank" rel="noopener" class="nav-link" href="https://x.com/mremoteng"><i class="bi bi-twitter"></i><span class="d-lg-none ms-2">{$t('header.x')}</span></a>
						</li>
						<li class="nav-item">
							<a target="_blank" rel="noopener" class="nav-link" href="https://mremoteng.readthedocs.io/"><i class="bi-file-text-fill"></i><span class="d-lg-none ms-2">{$t('header.documentation')}</span></a>
						</li>
						<li class="nav-item py-2 py-lg-1 col-12 col-lg-auto">
							<div class="vr d-none d-lg-flex h-100 mx-lg-2 text-white"></div>
							<hr class="d-lg-none my-2 text-white-50">
						</li>
						<div class="d-flex align-items-center">
  <LanguageSwitcher />
  <div class="d-lg-block mx-2" style="height: 24px;">
    <div class="vr h-100"></div>
  </div>
  <hr class="d-lg-none my-2 text-white-50">
  <ThemeSwitcher />
</div>




					</ul>
				</div>
				{#if mobileMenuOpen}
					<div class="mobile-nav" role="dialog" aria-modal="true">
						<button class="mobile-menu-close" on:click={closeMobileMenu} aria-label="Close menu">×</button>
							{#each menuItems as item}
								<a 
									href="{base}{item.path}" 
									on:click={closeMobileMenu}
									class:active={page.url.pathname === (base + item.path).replace(/\/$/, '') || (page.url.pathname === base && item.path === '/')}
								>
									{$t(item.titleKey)}
								</a>
							{/each}
					</div>
				{/if}
			</div>
		</div>
	</div>
</header>
