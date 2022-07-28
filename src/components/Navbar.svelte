<script lang="ts">
import { Styles } from 'sveltestrap';
import Fa from 'svelte-fa'
import { faBars } from '@fortawesome/free-solid-svg-icons'
import { faGraduationCap } from '@fortawesome/free-solid-svg-icons'
import { faCirclePlay } from '@fortawesome/free-solid-svg-icons'
import { faArrowRightLong } from '@fortawesome/free-solid-svg-icons'
import { faArrowLeftLong } from '@fortawesome/free-solid-svg-icons'

  import {
    Collapse,
    Navbar,
    NavbarToggler,
    NavbarBrand,
    Nav,
    NavItem,
    NavLink
  } from 'sveltestrap';

  const colors = [
    'dark'
  ];

  let isOpen = false;
  const toggle = () => (isOpen = !isOpen);
</script>

<div>
<Navbar color="dark" dark expand="md">
  <NavbarToggler on:click={toggle} class="me-2"><Fa icon={faBars}></Fa></NavbarToggler>
  <Collapse {isOpen} navbar>
    <Nav navbar>
      <NavItem>
        <NavLink href="#">Report a Bug</NavLink>
      </NavItem>
      <NavItem>
        <NavLink href="#">Help</NavLink>
      </NavItem>
    </Nav>
  </Collapse>
  <NavbarBrand href="/" class="me-auto"> <Fa icon={faCirclePlay}></Fa></NavbarBrand>
  <NavbarBrand href="/" class="me-auto"> <Fa icon={faGraduationCap}></Fa></NavbarBrand>
  <NavbarBrand href="/" class="me-auto"> <Fa icon={faArrowLeftLong}></Fa></NavbarBrand>
  <NavbarBrand href="/" class="me-auto"> <Fa icon={faArrowRightLong}></Fa></NavbarBrand>
</Navbar>
</div>
