# Skill: solid-architecture-expert

## Purpose
Analyze, refactor, and design mission-critical software architectures based on scientific evidence, SOLID Principles, quality metrics (CK and MOOD), and Cognitive-Driven Development (CDD). The goal is to reduce coupling, improve maintainability, and avoid cognitive overload.

## When to Use
When the user requests code reviews, new component design, technical debt mitigation, or legacy system refactoring.

## Mandatory Inquiry (Pre-requisites)
```text
# Via initial questionnaire (required before proposing solutions)
1. System Context: Programming language and typing paradigm.
2. Constraints: Performance requirements, extreme latency, or hardware coupling.
3. Backward Compatibility: Limits on modifying public interfaces due to legacy systems.
4. Scope: Is it new code, a legacy module, or a specific pipeline?
```
No architectural solution should be generated without clearly understanding these four variables.

### Accepted Exclusions (Trade-offs)

| Scenario | Rule | Why pure design is compromised |
| :--- | :--- | :--- |
| AI / Machine Learning | DIP (Dependency Inversion) | Low-level coupling (e.g., GPUs in TensorFlow) prioritizes latency over pure abstraction. |
| High-Scale Systems | Extreme SRP | Architectural purism can be compromised if it heavily penalizes real-time performance or massive batch processing. |
| Strict Legacy APIs | OCP / ISP | Ensuring strict backward compatibility with existing clients that cannot update contracts. |

*NEVER compromise a principle without justifying the trade-off (performance vs. purity) in the proposal.*

## Critical Rules: SOLID Principles Examples

### 1. Single Responsibility Principle (SRP)
A class should have one, and only one, reason to change.

```typescript
// GOOD — Atomic and cohesive entities
class InvoiceCalculator {
    calculateTotal(items: any[]): number {
        // Calculation logic
        return 0;
    }
}

class InvoiceRepository {
    save(invoice: any): void {
        // Database logic
    }
}

// BAD — "God Classes" (Logical monoliths)
class InvoiceSystemManager {
    calculateTotal(items: any[]): number { /* ... */ return 0; }
    saveToDb(invoice: any): void { /* ... */ }
    printInvoice(): void { /* ... */ }
}
```

### 2. Open/Closed Principle (OCP)
Software entities should be open for extension, but closed for modification.

```typescript
// GOOD — Extensible via Polymorphism
interface DiscountStrategy {
    apply(total: number): number;
}

class VIPDiscount implements DiscountStrategy {
    apply(total: number): number {
        return total * 0.8;
    }
}

// BAD — Hardcoded conditionals (requires modification for new types)
class DiscountCalculator {
    applyDiscount(total: number, customerType: string): number {
        if (customerType === "VIP") {
            return total * 0.8;
        } else if (customerType === "NORMAL") {
            return total * 0.95;
        }
        return total;
    }
}
```

### 3. Liskov Substitution Principle (LSP)
Subtypes must be substitutable for their base types without altering the correctness of the program.

```typescript
// GOOD — Respects Behavioral Contract
class Bird {
    // Base bird properties
}

class FlyingBird extends Bird {
    fly(): void { /* ... */ }
}

class Penguin extends Bird {
    // Penguins don't implement fly() and don't break contracts
}

// BAD — Unexpected Mutation or Exception
class BadBird {
    fly(): void { /* ... */ }
}

class BadPenguin extends BadBird {
    fly(): void {
        throw new Error("Penguins cannot fly!"); // Breaks LSP
    }
}
```

### 4. Interface Segregation Principle (ISP)
Clients should not be forced to depend upon interfaces that they do not use.

```typescript
// GOOD — Segregated, specific interfaces
interface IPrinter {
    printDoc(): void;
}

interface IScanner {
    scanDoc(): void;
}

// BAD — "Fat interfaces" (Overloads working memory)
interface IMachine {
    printDoc(): void;
    scanDoc(): void;
    faxDoc(): void;
}
```

### 5. Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions.

```typescript
// GOOD — Depends on abstractions (Interfaces)
interface IDatabase {
    save(data: any): void;
}

class OrderProcessor {
    private db: IDatabase;

    constructor(db: IDatabase) { // Injected dependency
        this.db = db;
    }
}

// BAD — Tightly Coupled to concrete implementations
class MySQLDatabase {
    save(data: any): void { /* ... */ }
}

class BadOrderProcessor {
    private db: MySQLDatabase;

    constructor() {
        this.db = new MySQLDatabase(); // Hardcoded dependency
    }
}
```

## Common Fixes (Impact on Metrics)

| Design Smell | Affected Metric | Fix (Refactoring) |
| :--- | :--- | :--- |
| "God Class" with multiple responsibilities | High WMC | Apply SRP to split the class into small, predictable entities. |
| Rigidly coupled components | High CBO | Introduce Interfaces (DIP and ISP) to reduce direct coupling. |
| Methods not sharing state | High LCOM | Restructure classes to increase functional and semantic cohesion. |
| Incomprehensible inheritance hierarchies | High DIT | Prioritize composition over inheritance to maintain flat hierarchies. |

## Cookbook

| If... | Then... |
| :--- | :--- |
| Diagnosing a problem | Identify the specific SOLID violation, map the symptoms, and state the cognitive impact and technical debt. |
| Proposing contracts (LSP) | Explicitly define: Preconditions, Postconditions, State Invariants, and History Constraints. |
| Delivering refactored code | Always provide two comparative blocks: "Before (Tightly Coupled)" and "After (SOLID Compliant)". |
| Evaluating projected impact | Show an analytical table estimating the evolution of CK and MOOD metrics (WMC, CBO, LCOM, DIT). |
| Identifying design risks | Warn about secondary consequences (e.g., more files) and suggest mitigation tactics (e.g., Ensemble/Example prompting). |