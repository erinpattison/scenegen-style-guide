# FIRST DRAFT
# SCENEGEN FRONTEND STYLE GUIDE (REACT/TYPESCRIPT)

## Table of Contents
1. [General Code Style](#1-general-code-style)
2. [File and Folder Structure](#2-file-and-folder-structure)
3. [Naming Conventions](#3-naming-conventions)
4. [React Component Structure](#4-react-component-structure)
5. [TypeScript Specific Guidelines](#5-typescript-specific-guidelines)
6. [Hooks and State Management](#6-hooks-and-state-management)
7. [Styling](#7-scss--styling-best-practices)
8. [Testing](#8-testing)
9. [Code Comments](#9-code-comments)
10. [Version Control and Git Practices](#10-version-control-and-git-practices)

---

## General Code Style

### 1.1 Formatting

- **Indentation**: Use 2 spaces for indentation.
- **Line Length**: Limit lines to a maximum of 100 characters.
- **Semicolons**: Always use semicolons ( ; ) at the end of statements.
- **Quotes**: Use single quotes for strings, unless using template literals for interpolation.
- **Trailing commas**: Use trailing commas for multiline objects, arrays, and functions:
    ```javascript
    const user = {
      id: 1,
      name: 'Chloe',
    };
    ```
- **Line Breaks**: Leave a blank line between blocks and before return statements for readability.

### 1.2 Variables

- **Use `const` for variables**: Declare variables with `const` by default, unless the value will be reassigned during the component’s lifecycle. Use state management (`useState`) for variables that change over time or affect the UI rendering.
    ```javascript
    const [count, setCount] = useState(0);
    
    const incrementCount = () => {
      setCount(count + 1);
    };
    ```
- **Use `let` only where necessary**: Use `let` for variables that are local to a function and do not trigger a re-render.
    ```javascript
    const sumArray = (arr: number[]) => {
      let sum = 0;
      for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
      }
      return sum;
    };
    ```

### 1.3 Arrow Functions

- Prefer arrow functions for anonymous functions, especially for inline event handlers or callbacks.
    ```javascript
    const handleClick = () => {
      console.log('Button clicked');
    };
    ```

### 1.4 Avoid `any`

- Avoid using `any` in TypeScript. Use specific types whenever possible to enhance type safety.

---

## File and Folder Structure

### 2.1 General Guidelines

- **Modular Design**: Organize files by feature or module (e.g. views) rather than by type (e.g. components, hooks).
- **SCSS Modularization**: Centralize globally used styles and use SCSS Modules for component-specific styles.
- **Shared components and hooks**: Place reusable UI components in the `components/` folder and reusable hooks in the `hooks/` folder.

### 2.2 Key Recommendations

- **Assets**: Store fonts and images in the `assets/` folder.
- **Components**: Place reusable UI components in the `components/` folder. Modularize component-specific styles to avoid conflicts.
- **Hooks**: Store reusable hooks in the `hooks/` folder, organized by functionality (e.g. `accountHooks/`, `utilityHooks/`).
- **Redux Store**: Organize Redux-related logic under `store/` (e.g. actions, reducers).
- **Views (Routes)**: Organize each view (e.g. `account/`, `bookkeeping/`) by feature, containing components, pages, and SCSS styles for modularity.

### 2.3 Example Component Folder Structure

For the `account/` view, organize related components, pages, and styles like this:

```plaintext
src/ 
  views/
    account/
      components/
        StatelessOnboard.tsx
        OnboardForm.tsx
      Account.tsx
      Onboard.tsx
      _account.scss
      _onboarding.scss
```
## 3. Naming Conventions

### 3.1 Component Names
- Use PascalCase for components and class names.
    ```typescript
    const UserProfile = () => {
      return <div>User Profile</div>;    
    };
    ```

### 3.2 Variables and Functions
- Use camelCase for variables and functions.
- Use descriptive names for variables and functions.
    ```typescript
    const fetchUserData = async () => {
      /* … */    
    };
    ```

### 3.3 Constants
- Use ALL_CAPS for constants.
    ```typescript
    const API_URL = 'https://api.example.com';
    ```

---

## 4. React Component Structure

### 4.1 Functional Components
- Always use functional components. Avoid class components.
    ```typescript
    const UserProfile: React.FC = () => {
      return <div>User Profile</div>;
    };
    ```

### 4.2 Prop Destructuring
- Destructure props directly in the function signature.
    ```typescript
    const UserProfile = ({ user }) => {
      return <div>{user.name}</div>;
    };
    ```

### 4.3 Self-Closing Tags
- Use self-closing tags when a component has no children.
    ```tsx
    <Button />
    ```

### 4.4 Return Statements
- Avoid unnecessary parentheses around JSX return statements, unless the JSX spans multiple lines.
    ```typescript
    return <div>Hello</div>;
    
    return (
      <div>
        <h1>Hello</h1>
        <p>Welcome</p>
      </div>
    );
    ```

---

## 5. TypeScript Specific Guidelines

### 5.1 Define Explicit Types
- Always define explicit types for props, state, and functions.
    ```typescript
    interface User {
      id: number;
      name: string;
    }

    const UserProfile = ({ user }: { user: User }) => {
      return <div>{user.name}</div>;
    };
    ```

### 5.2 Avoid `any`
- Avoid using `any`. Use generics or unions instead if unsure.
    ```typescript
    const fetchData = async <T>(): Promise<T> => {
      // …
    };
    ```

### 5.3 Enum over literal types
- Use enums for a set of related constants.
    ```typescript
    enum UserRole {
      Admin = 'admin',
      User = 'user',
    }
    ```

---

## 6. Hooks and State Management

### 6.1 Custom Hooks
- Preface custom hook names with `use`.
    ```typescript
    const useFetchData = (url: string) => { /* … */ };
    ```

### 6.2 State Initialization
- Initialize state with sensible defaults.
    ```typescript
    const [user, setUser] = useState<User | null>(null);
    ```

---

## 7. SCSS & Styling Best Practices

### 7.1 General Guidelines

- **Framework Precedence**: The chosen CSS framework will take precedence over custom styles. SCSS will supplement it.
- **Variables**: Use SCSS variables for managing shared values (i.e., colors, spacing, typography). Do not use mixins.
- **Nested Styles**: Use nested styles where appropriate.
- **Page-Specific SCSS Files**: Each page should have its own SCSS file.

### 7.2 Variable-Driven Styling

- Use SCSS variables to ensure consistency and easy maintenance.
    ```scss
    $primary-color: #000;
    $secondary-color: #fff;
    $font-size-base: 16px;
    $spacing-unit: 8px;
    ```

- Combine SCSS variables with framework classes.
    ```scss
    .header {
      background-color: $primary-color;
      padding: $spacing-unit * 2;
      font-size: $font-size-base;

      .framework-btn {
        margin-top: $spacing-unit;
      }
    }
    ```

### 7.3 SCSS Folder Structure

- Organize global and page-specific styles:
    ```
    src/
      components/
        layout/
          header/
            _appHeader.scss
          sidebar/
            _sidebar.scss
        _layout.scss
      scss/
        _variables.scss
        _custom.scss
        style.scss
    ```

### 7.4 SCSS Conventions

- Follow the **BEM naming convention**:
    ```scss
    .button {
      &__icon {
        margin-right: $spacing-unit;
      }
      &--primary {
        background-color: $primary-color;
      }
    }
    ```

### 7.5 Responsive Design

- Supplement the framework’s utilities with media queries for custom components.
    ```scss
    $breakpoint-mid: 768px;

    .container {
      width: 100%;

      @media (min-width: $breakpoint-mid) {
        width: 80%;
      }
    }
    ```

### 7.6 Specificity and Avoiding `!important`

- Avoid `!important` whenever possible, relying on simple selectors and framework utilities to maintain low specificity.

---

## 8. Testing

### 8.1 Test File Naming

- Name test files as `ComponentName.test.tsx` and place them alongside the component:
    ```
    src/components/Button/Button.test.tsx
    ```

### 8.2 Testing Libraries

- Use React Testing Library and Jest for unit tests.
    ```typescript
    test('renders the button', () => {
      render(<Button />);
      expect(screen.getByRole('button')).toBeInTheDocument();
    });
    ```

---

## 9. Code Comments

### 9.1 Comment Types

- Use JSDoc for functions and complex logic:
    ```typescript
    /**
     * Fetches user data from the API
     * @param id - the ID of the user
     * @returns A promise with the user data
     */
    const fetchUser = (id: number) => { /* … */ };
    ```

### 9.2 Avoid Redundant Comments

- Avoid unnecessary or redundant comments.
    ```typescript
    // Bad: This is redundant
    // This function fetches data
    const fetchData = () => { /* … */ };
    ```

---

## 10. Version Control and Git Practices

### 10.1 Branching

- Use feature branches with descriptive names (e.g., `feature/user-auth`).
- Always create branches for new work.

### 10.2 Commit Messages

- Use clear and descriptive commit messages:
    ```plaintext
    git commit -m "Fix user authentication redirect issue"
    ```

### 10.3 Pull Requests

- Submit pull requests for all features, and assign at least one reviewer.
