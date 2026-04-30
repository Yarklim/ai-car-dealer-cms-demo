import { defineConfig, globalIgnores } from 'eslint/config';
import nextVitals from 'eslint-config-next/core-web-vitals';
import nextTs from 'eslint-config-next/typescript';

export default defineConfig([
  // Базовые пресеты Next + React + Core Web Vitals
  ...nextVitals,
  // TS-правила из eslint-config-next/typescript
  ...nextTs,

  // Общие правила для проекта
  {
    rules: {
      // Глобальные core-правила (без сортировки импортов)
      'no-duplicate-imports': 'error',
      // 'no-console': ['warn', { allow: ['warn', 'error'] }],
      eqeqeq: ['error', 'smart'],
      curly: ['error', 'multi-line'],

      // React 19 / react hooks: отключаем слишком агрессивное правило
      'react-hooks/set-state-in-effect': 'off',

      // Стиль
      'prefer-const': 'error',
    },
  },

  // Override для TypeScript-файлов - только TS-версия no-unused-vars
  {
    files: ['**/*.{ts,tsx}'],
    rules: {
      'no-unused-vars': 'off',
      '@typescript-eslint/no-unused-vars': [
        'warn',
        {
          argsIgnorePattern: '^_',
          varsIgnorePattern: '^_',
        },
      ],
    },
  },

  // FSD: страницы - только публичные API
  {
    files: ['src/app/**/*.{ts,tsx}'],
    rules: {
      'no-restricted-imports': [
        'error',
        {
          patterns: [
            '@features/*/ui/*',
            '@features/*/api/*',
            '@features/*/model/*',
            '@features/*/hooks/*',
            '@features/*/utils/*',
            '@features/*/internal/*',
            '@entities/*/ui/*',
            '@entities/*/api/*',
            '@entities/*/model/*',
            '@entities/*/hooks/*',
            '@entities/*/utils/*',
            '@entities/*/internal/*',
            '@widgets/*/ui/*',
            '@widgets/*/model/*',
            '@widgets/*/hooks/*',
            '@widgets/*/utils/*',
            '@widgets/*/internal/*',
            '../../features/*',
            '../../entities/*',
            '../../widgets/*',
          ],
        },
      ],
    },
  },

  // shared - фундамент: не тянет верхние слои
  {
    files: ['src/shared/**/*.{ts,tsx}'],
    rules: {
      'no-restricted-imports': [
        'error',
        {
          patterns: [
            '@features/*',
            '@widgets/*',
            '@entities/*',
            '../../features/*',
            '../../widgets/*',
            '../../entities/*',
          ],
        },
      ],
    },
  },

  // features - не лазит во внутренности других features (разрешён только их public)
  {
    files: ['src/features/**/*.{ts,tsx}'],
    rules: {
      'no-restricted-imports': [
        'error',
        {
          patterns: [
            '@features/*/ui/*',
            '@features/*/api/*',
            '@features/*/model/*',
            '@features/*/hooks/*',
            '@features/*/utils/*',
            '@features/*/internal/*',
          ],
        },
      ],
    },
  },

  // widgets - только публичные API features/entities
  {
    files: ['src/widgets/**/*.{ts,tsx}'],
    rules: {
      'no-restricted-imports': [
        'error',
        {
          patterns: [
            '@features/*/ui/*',
            '@features/*/api/*',
            '@features/*/model/*',
            '@features/*/hooks/*',
            '@features/*/utils/*',
            '@features/*/internal/*',
            '@entities/*/ui/*',
            '@entities/*/api/*',
            '@entities/*/model/*',
            '@entities/*/hooks/*',
            '@entities/*/utils/*',
            '@entities/*/internal/*',
          ],
        },
      ],
    },
  },

  // Client vs Server: разруливаем запрещённые импорты/глобалы
  {
    files: ['src/**/*.client.{ts,tsx}'],
    rules: {
      'no-restricted-imports': [
        'error',
        {
          paths: [
            {
              name: 'next/headers',
              message: 'Нельзя использовать next/headers в client-компонентах',
            },
            {
              name: 'next/server',
              message: 'next/server — только на сервере',
            },
          ],
          patterns: ['**/*.server.*'],
        },
      ],
    },
  },
  {
    files: ['src/**/*.server.{ts,tsx}'],
    rules: {
      'no-restricted-globals': [
        'error',
        { name: 'window', message: 'window недоступен на сервере' },
        { name: 'document', message: 'document недоступен на сервере' },
      ],
    },
  },

  // Игнор служебных директорий/файлов
  globalIgnores(['.next/**', 'out/**', 'build/**', 'next-env.d.ts']),
]);
