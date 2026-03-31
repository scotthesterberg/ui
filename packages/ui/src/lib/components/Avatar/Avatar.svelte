<script lang="ts">
  import { mdiPaw } from '$lib/icons/index.js';
  import type { Size } from '$lib/types.js';
  import { cleanClass } from '$lib/utilities/internal.js';
  import { tv } from 'tailwind-variants';
  import Icon from '../Icon/Icon.svelte';

  type Props = {
    size?: Size;
    color?: 'primary' | 'pink' | 'red' | 'yellow' | 'blue' | 'green' | 'purple' | 'orange' | 'gray' | 'amber';
    name: string;
    entityType?: 'user' | 'pet';
    class?: string;
  };

  const { color = 'primary', size = 'medium', name, entityType = 'user', class: className }: Props = $props();

  const styles = tv({
    base: 'flex items-center overflow-hidden rounded-full align-middle text-white shadow-md',
    variants: {
      color: {
        primary: 'bg-primary text-light',
        pink: 'bg-pink-400',
        red: 'bg-red-500',
        yellow: 'bg-yellow-500',
        purple: 'bg-purple-600',
        orange: 'bg-orange-600',
        gray: 'bg-gray-600',
        amber: 'bg-amber-600',
        blue: 'bg-blue-500',
        green: 'bg-green-600',
      },
      size: {
        tiny: 'h-5 w-5 text-xs',
        small: 'h-7 w-7 text-sm',
        medium: 'h-10 w-10 text-base',
        large: 'h-12 w-12 text-lg',
        giant: 'h-16 w-16 text-xl',
      },
    },
  });

  const getInitials = (name: string) => {
    return name
      .split(' ')
      .map((part) => part.at(0))
      .join('')
      .substring(0, 2)
      .toUpperCase();
  };

  const initials = $derived(getInitials(name));

  const iconSize: Record<Size, string> = {
    tiny: '0.8rem',
    small: '1rem',
    medium: '1.5rem',
    large: '2rem',
    giant: '2.5rem',
  };
</script>

<figure class={cleanClass(styles({ size, color }), className)}>
  {#if entityType === 'pet'}
    <div class="flex h-full w-full items-center justify-center">
      <Icon icon={mdiPaw} size={iconSize[size]} />
    </div>
  {:else}
    <span class="w-full text-center font-medium select-none">{initials}</span>
  {/if}
</figure>
