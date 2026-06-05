# Amazon LLD (Low-Level Design) Interview Preparation Guide

**Compiled from public Amazon interview experiences (LeetCode Discuss, GeeksforGeeks, Blind, Medium, Substack) — last ~12 months. Updated May 2026.**

This guide covers the LLD problems most frequently reported in Amazon SDE-1, SDE-2, and SDE-3 / L5–L6 loops, with structured answers (requirements → entities/classes → design patterns → key code skeletons → edge cases / follow-ups).

---

## Table of Contents

1. How the Amazon LLD round actually works
2. The mental framework (use this for every problem)
3. Design patterns you MUST know cold
4. The 25 most-asked Amazon LLD problems (with answers)
   - Tier 1 — Highest frequency (drill these first)
     1. Parking Lot
     2. BookMyShow / Movie Ticket Booking
     3. Elevator System
     4. LRU Cache
     5. Vending Machine
     6. Amazon Locker
   - Tier 2 — Common
     7. Splitwise
     8. Notification Service
     9. Logging Framework (log4j-style)
     10. Rate Limiter
     11. Stack Overflow
     12. Tic Tac Toe
     13. Chess
     14. ATM
     15. Snake & Ladder
   - Tier 3 — Asked, less frequent
     16. Hotel / OYO booking
     17. Library Management
     18. Food Ordering (Swiggy / Zomato / DoorDash)
     19. Online Shopping Cart (Amazon)
     20. Ride-sharing (Uber)
     21. Music Streaming (Spotify)
     22. Meeting Room Scheduler
     23. URL Shortener (TinyURL)
     24. File System / In-memory FS
     25. Customer-Support Ticketing
5. Concurrency / multithreading add-ons Amazon loves to ask
6. Behavioral wrapping: LP signals interviewers look for in LLD rounds
7. 4-week study plan + resources

---

## 1) How the Amazon LLD round actually works

Based on recent (2024 – early 2026) Amazon SDE-2 / L5 interview write-ups:

- **It is a separate round for SDE-2 and above.** SDE-1 loops occasionally include an LLD-flavored coding problem (e.g. "design a vending machine, then code it"), but the dedicated LLD round is standard from SDE-2.
- **Duration:** ~45 min technical + ~15 min Leadership Principles (LPs). Some bar-raisers do an LLD + DSA mix.
- **Format:** Open-ended prompt → you gather requirements → propose entities/classes → write working code (compilable, runnable, often with a `main` driver). Many candidates report they were expected to **actually run the code** by the end.
- **What gets you rejected (from real "rejected" write-ups):**
  - Jumping to code without clarifying requirements.
  - One God-class with all logic in it.
  - Hard-coded behavior where strategy/state/factory was obvious.
  - No concurrency thinking when the problem clearly needs it (parking lot, locker, elevator).
  - Not handling edge cases (full lot, no available agent, payment failure).
  - Inability to extend the design when the interviewer adds a twist ("now support events along with movies", "now support multiple cities").
- **What gets you a hire:**
  - Crisp 2-min requirement gathering (functional + non-functional).
  - Naming entities cleanly, identifying which classes own which state.
  - Picking the **right** pattern, not the most patterns.
  - Writing extensible interfaces; showing how a new requirement plugs in.
  - Talking about thread safety even when not asked.

---

## 2) The mental framework — use this for EVERY problem

I recommend the same 6-step skeleton in every LLD interview. It's slow at first; after 5–6 practice runs it becomes automatic.

### Step 1 — Clarify requirements (3–5 min)
Ask in 4 buckets:
- **Operations:** what actions does the user perform? (park car, book ticket, send notification…)
- **Actors:** who interacts with the system? (customer, admin, agent, system itself)
- **Constraints / scale:** size, concurrency, multi-tenant, single machine vs distributed?
- **Out-of-scope:** UI, payment processor internals, persistence, auth — confirm what you can skip.

Write them down on the shared editor so the interviewer can object early.

### Step 2 — Identify core entities
Scan the requirements for nouns. Filter: does it hold state or enforce rules? → it's an entity. Otherwise it's probably an attribute.

### Step 3 — Define class responsibilities (Tell, Don't Ask)
Each class owns its own state and exposes behavior. Avoid giving everything to a `Manager` class.

### Step 4 — Pick design patterns deliberately
The most useful 6 for LLD interviews:
- **Strategy** — pluggable algorithm (parking-spot allocation, agent assignment, pricing).
- **Observer** — fan-out events (notifications, stats updates).
- **Factory** — create instances based on type (vehicle, chess piece, payment method).
- **Singleton** — single instance (logger, config, parking lot itself).
- **State** — object behavior changes with state (vending machine, elevator, order).
- **Decorator** — layer behavior (pizza toppings, coffee add-ons, notifications channels).

### Step 5 — Write code
- Interfaces first, then concrete classes.
- Put validations inside the entity that owns the data.
- Use enums for closed sets (`SpotType`, `VehicleType`, `OrderStatus`).
- Use `ConcurrentHashMap`, `AtomicInteger`, `ReentrantLock` where state is shared.

### Step 6 — Discuss extensions
Volunteer extensions before the interviewer asks: "If we wanted to add X, we'd plug it in here because of the Strategy interface." This is what bar-raisers reward.

---

## 3) Design patterns you MUST know cold

| Pattern    | One-line trigger                                              | Amazon problems where it shines               |
| ---------- | ------------------------------------------------------------- | --------------------------------------------- |
| Strategy   | "Multiple ways to do the same operation"                      | Parking allocation, agent assignment, pricing |
| Observer   | "When X happens, notify N parties"                            | Notification service, stock alerts, logger    |
| Factory    | "Create different concrete classes from a type/string"        | Vehicle, chess piece, payment, notification   |
| Singleton  | "One global instance, lazy init, thread safe"                 | Logger, config, ParkingLot                    |
| State      | "Object behaves differently depending on its current state"   | Vending machine, elevator, order, ATM         |
| Decorator  | "Stack optional behaviors at runtime"                         | Pizza, coffee, notification channels          |
| Chain of Responsibility | "Pass a request along handlers until one handles it" | Logger levels, ATM cash dispenser, support ticket escalation |
| Command    | "Encapsulate a request as an object (undo/queue/retry)"       | Job scheduler, remote control, transactions   |
| Composite  | "Tree structure where leaves and groups are treated the same" | File system, menu, organization               |
| Builder    | "Object with many optional fields, immutable result"          | Notification, HTTP request, complex orders    |

Memorize **Strategy + Observer + Factory + Singleton + State** at minimum — those five cover ~80% of Amazon LLD answers.

---

## 4) The 25 most-asked Amazon LLD problems

For each problem I give:
- **Requirements** to lock in.
- **Core classes** to declare.
- **Patterns** to use and why.
- **Code skeleton** (Java — translate to your language).
- **Common follow-ups** the interviewer adds.

---

### TIER 1 — Drill these first

---

#### 4.1 Parking Lot (most frequently asked Amazon LLD problem)

**Requirements**
- Multi-floor lot; each floor has multiple spots; spot types: `BIKE`, `COMPACT`, `LARGE`, `HANDICAP`, `ELECTRIC`.
- Vehicle types map to spot types (a Truck needs LARGE, a Car can use COMPACT or LARGE).
- Park / unpark; issue ticket on entry; compute fee on exit.
- Multiple entry/exit gates; **concurrent** parking must be safe.
- Pluggable allocation strategy (nearest-to-entrance, best-fit, first-available).
- Out of scope: payment processor internals, persistence.

**Core classes**
`ParkingLot` (singleton), `ParkingFloor`, `ParkingSpot` (abstract) → `BikeSpot`, `CompactSpot`, `LargeSpot`, `Vehicle` (abstract) → `Car`, `Truck`, `Bike`, `Ticket`, `EntryGate`, `ExitGate`, `ParkingStrategy` (interface), `FeeStrategy` (interface).

**Patterns**
- **Singleton** — `ParkingLot`.
- **Strategy** — `ParkingStrategy`, `FeeStrategy`.
- **Factory** — create spot/vehicle by type.
- **State** — spot state: `FREE` / `OCCUPIED` / `RESERVED`.

**Skeleton (Java)**

```java
enum VehicleType { BIKE, CAR, TRUCK }
enum SpotType { BIKE, COMPACT, LARGE }

abstract class Vehicle {
    String plate; VehicleType type;
    Vehicle(String plate, VehicleType type) { this.plate = plate; this.type = type; }
}
class Car extends Vehicle { Car(String p) { super(p, VehicleType.CAR); } }

class ParkingSpot {
    String id; SpotType type;
    private final AtomicReference<Vehicle> occupant = new AtomicReference<>();
    boolean park(Vehicle v) { return occupant.compareAndSet(null, v); }   // CAS = thread safe
    boolean isFree()        { return occupant.get() == null; }
    Vehicle vacate()        { return occupant.getAndSet(null); }
}

interface ParkingStrategy {
    Optional<ParkingSpot> findSpot(List<ParkingFloor> floors, Vehicle v);
}
class NearestFirstStrategy implements ParkingStrategy { /* iterate floors top→bottom */ }
class BestFitStrategy     implements ParkingStrategy { /* smallest spot that fits */ }

interface FeeStrategy { double compute(Ticket t); }
class HourlyFeeStrategy implements FeeStrategy { /* hours * rate-by-type */ }

class ParkingLot {                                 // SINGLETON
    private static final ParkingLot INSTANCE = new ParkingLot();
    public  static ParkingLot get() { return INSTANCE; }
    private final List<ParkingFloor> floors = new CopyOnWriteArrayList<>();
    private final ParkingStrategy strategy   = new NearestFirstStrategy();
    private final FeeStrategy     feeStrategy = new HourlyFeeStrategy();

    public synchronized Optional<Ticket> park(Vehicle v) {
        return strategy.findSpot(floors, v).map(spot -> {
            spot.park(v);
            return new Ticket(v, spot, Instant.now());
        });
    }
    public double unpark(Ticket t) {
        t.spot.vacate();
        return feeStrategy.compute(t);
    }
}
```

**Follow-ups**
- "Two cars enter different gates and the lot has 1 spot left." → CAS on `ParkingSpot.occupant`, retry in strategy if loss.
- "Add monthly subscribers / reserved spots." → `SpotState.RESERVED` + `Reservation` table.
- "Different fee for weekends / EV charging." → another `FeeStrategy`.
- "Make it work for airport scale (multiple lots)." → `ParkingLotRegistry` keyed by lotId.

---

#### 4.2 BookMyShow / Movie Ticket Booking

**Requirements**
- Cities → cinemas → screens → shows (movie + screen + time).
- Each show has seats in different tiers (`SILVER`, `GOLD`, `PLATINUM`) with different prices.
- User can search movies, view available seats, hold seats, pay, and confirm.
- **Two users cannot book the same seat** — concurrency-critical.
- Cancellation with refund.

**Core classes**
`City`, `Cinema`, `Screen`, `Show`, `Movie`, `Seat`, `Booking`, `User`, `Payment`, `SeatLock`, `BookingService`.

**Patterns**
- **Singleton** — `BookingService`.
- **State** — `Booking`: `CREATED → PAYMENT_PENDING → CONFIRMED / CANCELLED / EXPIRED`.
- **Strategy** — pricing (weekend vs weekday), seat-recommendation.
- **Observer** — notify users on booking confirmation / cancellation.

**Key idea: Seat-locking service**
Booking a seat is two-phase:
1. Lock seat with a short TTL (5 min) — exclusive per (show, seat).
2. Confirm after successful payment, else release on TTL expiry.

```java
class SeatLockProvider {
    private final Map<String, SeatLock> locks = new ConcurrentHashMap<>();
    private final long ttlMs;

    boolean lockSeats(Show s, List<Seat> seats, User u) {
        long now = System.currentTimeMillis();
        synchronized (s) {                                 // per-show lock
            for (Seat seat : seats) {
                SeatLock l = locks.get(key(s, seat));
                if (l != null && !l.isExpired(now)) return false;
            }
            for (Seat seat : seats)
                locks.put(key(s, seat), new SeatLock(u, now + ttlMs));
            return true;
        }
    }
    void confirm(Show s, List<Seat> seats) { /* mark booked, drop lock */ }
    void release(Show s, List<Seat> seats) { seats.forEach(x -> locks.remove(key(s, x))); }
    private String key(Show s, Seat x)     { return s.id + "#" + x.id; }
}
```

**Follow-ups**
- "Now support live events (concerts) alongside movies." → introduce abstract `Show`/`Event` and `Performable` interface; pricing, seating, and booking flow stay the same.
- "Dynamic pricing (surge)." → strategy.
- "Group booking — all-or-nothing." → wrap lock in transaction; rollback if any fail.

---

#### 4.3 Elevator System (asked in Amazon SDE-2 BLR & Spain, 2025)

**Requirements**
- Building with N floors, M elevators.
- External request: floor + direction (UP / DOWN).
- Internal request: passenger inside picks destination floor.
- Need a **scheduler** that picks which elevator serves which request.
- Elevator has states: `IDLE`, `MOVING_UP`, `MOVING_DOWN`, `MAINTENANCE`.

**Core classes**
`Building`, `Elevator`, `ElevatorController` (scheduler), `Request` (`ExternalRequest`, `InternalRequest`), `Direction` enum, `ElevatorState` enum, `DispatchStrategy`.

**Patterns**
- **State** — elevator behavior depends on state.
- **Strategy** — `DispatchStrategy` (nearest-car, LOOK, SCAN).
- **Command** — each request is a command put on a queue.
- **Observer** — floors observe elevator arrival.

**Scheduler (LOOK algorithm sketch)**

```java
class Elevator {
    int id, currentFloor;
    Direction direction = Direction.IDLE;
    TreeSet<Integer> upRequests   = new TreeSet<>();
    TreeSet<Integer> downRequests = new TreeSet<>(Comparator.reverseOrder());

    void step() {
        if (direction == Direction.UP) {
            Integer next = upRequests.ceiling(currentFloor);
            if (next == null) { direction = downRequests.isEmpty() ? Direction.IDLE : Direction.DOWN; return; }
            currentFloor++; if (currentFloor == next) { open(); upRequests.remove(next); }
        } else if (direction == Direction.DOWN) {
            // symmetric
        }
    }
}

class ElevatorController {
    List<Elevator> elevators;
    Elevator pick(ExternalRequest r) {
        // score = distance + direction match + load; return min
        return elevators.stream().min(Comparator.comparingInt(e -> score(e, r))).get();
    }
}
```

**Follow-ups**
- "Express elevator that skips odd floors." → subclass / strategy.
- "Emergency mode — all elevators go to ground." → broadcast event; state machine forces override.
- "How would you test this?" — discuss simulation harness.

---

#### 4.4 LRU Cache

**Requirements**
- Fixed capacity. `get(k)` and `put(k,v)` both **O(1)**.
- Evict least-recently-used on overflow.

**Core idea**
HashMap + Doubly Linked List. Head = most recent, tail = LRU.

```java
class LRUCache<K, V> {
    private final int capacity;
    private final Map<K, Node<K,V>> map = new HashMap<>();
    private final Node<K,V> head = new Node<>(null, null), tail = new Node<>(null, null);

    static class Node<K,V> { K k; V v; Node<K,V> prev, next;
        Node(K k, V v){this.k=k; this.v=v;} }

    public LRUCache(int cap){ this.capacity = cap; head.next = tail; tail.prev = head; }

    public synchronized V get(K k) {
        Node<K,V> n = map.get(k);
        if (n == null) return null;
        remove(n); addFirst(n);
        return n.v;
    }
    public synchronized void put(K k, V v) {
        if (map.containsKey(k)) { Node<K,V> n = map.get(k); n.v = v; remove(n); addFirst(n); return; }
        if (map.size() == capacity) {
            Node<K,V> lru = tail.prev; remove(lru); map.remove(lru.k);
        }
        Node<K,V> n = new Node<>(k, v); map.put(k, n); addFirst(n);
    }
    private void addFirst(Node<K,V> n){ n.next=head.next; n.prev=head; head.next.prev=n; head.next=n; }
    private void remove(Node<K,V> n){ n.prev.next=n.next; n.next.prev=n.prev; }
}
```

**Follow-ups**
- "Make it thread-safe but with finer-grained locks." → segment locks like ConcurrentHashMap, or `ReadWriteLock`.
- "Now make it LFU." → different DS — frequency map + tie-break by recency (HashMap<freq, LinkedHashSet>).
- "Add TTL." → store expiry; lazy or eager eviction with `DelayQueue`.

---

#### 4.5 Vending Machine (asked in Amazon SDE-1 & SDE-2 multiple times)

**Requirements**
- Inventory of products (snacks/drinks) with prices and counts.
- States: `IDLE → ITEM_SELECTED → CASH_INSERTED → DISPENSING → CHANGE_RETURNED → IDLE`.
- Accept coins/notes; return change minimally (denominations problem).
- Refund if user cancels mid-flow.
- Maintenance: restock, collect cash.

**Patterns**
- **State** — the whole machine; transitions are explicit.
- **Strategy** — change-making (greedy vs DP).
- **Singleton** — machine.

```java
interface VendingState {
    void selectItem(VendingMachine m, String code);
    void insertCash(VendingMachine m, int amount);
    void dispense(VendingMachine m);
    void cancel(VendingMachine m);
}
class IdleState implements VendingState { /* only selectItem is valid */ }
class ItemSelectedState implements VendingState { /* only insertCash / cancel */ }
class CashInsertedState implements VendingState { /* only dispense / cancel */ }

class VendingMachine {
    VendingState state = new IdleState();
    Inventory inventory; int balance = 0; Item selected;
    void setState(VendingState s){ this.state = s; }
    public void selectItem(String code){ state.selectItem(this, code); }
    public void insertCash(int amt)   { state.insertCash(this, amt); }
    public void dispense()             { state.dispense(this); }
    public void cancel()               { state.cancel(this); }
}
```

**Follow-ups**
- "Card payment + UPI." → add `PaymentStrategy`; state goes `CASH_INSERTED → PAYMENT_PROCESSING`.
- "No exact change available." → reject + refund vs allow + credit note.

---

#### 4.6 Amazon Locker (asked recurrently in Amazon loops)

**Requirements**
- Locker stations with lockers of sizes `S`, `M`, `L`, `XL`.
- Package arrives at a station → assign smallest available locker that fits.
- Generate one-time code for customer; expires in 3 days.
- If not picked, return package to warehouse and free locker.

**Core classes**
`LockerStation`, `Locker`, `Package`, `Customer`, `Code` (one-time), `LockerAllocationStrategy`, `LockerService` (singleton).

**Patterns**
- **Strategy** — allocation (best-fit by size).
- **Observer** — listener for "code expired".
- **State** — locker: `AVAILABLE / OCCUPIED / EXPIRED / OUT_OF_SERVICE`.

```java
class LockerService {
    Optional<Locker> assign(Package p, LockerStation s) {
        return s.lockers.stream()
            .filter(l -> l.state == State.AVAILABLE && l.size.fits(p.size))
            .min(Comparator.comparing(l -> l.size))
            .map(l -> { l.assign(p, codeGen.next(), Instant.now().plus(Duration.ofDays(3))); return l; });
    }
    @Scheduled void sweepExpired() {
        for (Locker l : allLockers) if (l.isExpired()) { returnToWarehouse(l.package); l.free(); }
    }
}
```

**Follow-ups**
- "Optimization: pick station closest to delivery address." → out of LLD scope (HLD), but mention.
- "Concurrent assignment." → CAS on `Locker.state`.

---

### TIER 2 — Common

---

#### 4.7 Splitwise

**Requirements**
- Users, groups, expenses.
- Expense split types: `EQUAL`, `EXACT`, `PERCENT`, `SHARE`.
- Compute balance per user; show "who owes whom".
- Settle up; ideally simplify debts (`A→B 10, B→C 10` ⇒ `A→C 10`).

**Patterns**
- **Strategy** — `SplitStrategy` (EQUAL, EXACT, PERCENT…).
- **Observer** — notify members of new expenses.
- **Factory** — create strategy from enum.

```java
interface SplitStrategy { Map<User, Double> split(double total, List<User> users, Map<User,Double> params); }
class EqualSplit  implements SplitStrategy { /* total/n each */ }
class ExactSplit  implements SplitStrategy { /* sum of params must == total */ }
class PercentSplit implements SplitStrategy{ /* params sum to 100 */ }

class ExpenseService {
    private final Map<User, Map<User, Double>> balances = new HashMap<>();
    void addExpense(User payer, double amt, List<User> users, SplitStrategy strat, Map<User,Double> params){
        Map<User, Double> shares = strat.split(amt, users, params);
        for (var e : shares.entrySet()) {
            if (e.getKey().equals(payer)) continue;
            balances.computeIfAbsent(e.getKey(), x -> new HashMap<>()).merge(payer,  e.getValue(),  Double::sum);
            balances.computeIfAbsent(payer,    x -> new HashMap<>()).merge(e.getKey(), -e.getValue(), Double::sum);
        }
    }
}
```

**Follow-ups**
- "Simplify debts" — graph cycle removal / minimize edges via greedy max-debt match.

---

#### 4.8 Notification Service

**Requirements**
- Send notifications via multiple channels: `EMAIL`, `SMS`, `PUSH`, `IN_APP`.
- User preferences (which channels).
- Retry on failure with backoff; rate-limit per user.
- Templates with parameters.

**Patterns**
- **Strategy / Factory** — channel-specific sender.
- **Observer / Pub-Sub** — events → subscribers (notification dispatchers).
- **Decorator** — add retry, logging, rate-limiting around a sender.
- **Builder** — construct `Notification` (many optional fields).

```java
interface NotificationChannel { void send(Notification n); }
class EmailChannel implements NotificationChannel { public void send(Notification n){ /*...*/ } }
class SmsChannel   implements NotificationChannel { public void send(Notification n){ /*...*/ } }

class RetryDecorator implements NotificationChannel {
    private final NotificationChannel inner; private final int maxRetries;
    public void send(Notification n) {
        for (int i = 0; i < maxRetries; i++)
            try { inner.send(n); return; }
            catch (Exception e) { sleep(backoff(i)); }
        deadLetter(n);
    }
}
class NotificationService {
    Map<ChannelType, NotificationChannel> channels;
    void notify(User u, Notification n) {
        for (ChannelType t : u.preferences)
            channels.get(t).send(n);
    }
}
```

---

#### 4.9 Logging Framework (log4j-style)

**Requirements**
- Levels: `DEBUG < INFO < WARN < ERROR < FATAL`.
- Multiple sinks: console, file, remote.
- Configurable per-package level.
- Thread-safe.
- Async option.

**Patterns**
- **Chain of Responsibility** — level filters pass message to next handler.
- **Singleton** — `LoggerFactory`.
- **Strategy / Composite** — appender selection.

```java
enum Level { DEBUG, INFO, WARN, ERROR, FATAL }
interface Appender { void append(LogMessage m); }
class ConsoleAppender implements Appender { /* ... */ }
class FileAppender    implements Appender { /* synchronized write or async queue */ }

abstract class LogHandler {
    LogHandler next; Level level;
    public final void handle(LogMessage m) {
        if (m.level.ordinal() >= this.level.ordinal()) write(m);
        if (next != null) next.handle(m);
    }
    protected abstract void write(LogMessage m);
}
```

---

#### 4.10 Rate Limiter

**Requirements**
- Allow N requests per user per window.
- Algorithms to know: **Fixed Window**, **Sliding Window Log**, **Sliding Window Counter**, **Token Bucket**, **Leaky Bucket**.
- Per-user, per-IP, or per-API.

**Patterns**
- **Strategy** — algorithm pluggable.

```java
interface RateLimiter { boolean allow(String key); }

class TokenBucket implements RateLimiter {
    private final long capacity, refillPerSec;
    private final Map<String, Bucket> buckets = new ConcurrentHashMap<>();
    static class Bucket { double tokens; long lastRefillNanos; }
    public boolean allow(String key) {
        Bucket b = buckets.computeIfAbsent(key, k -> { Bucket x=new Bucket(); x.tokens=capacity; x.lastRefillNanos=System.nanoTime(); return x; });
        synchronized (b) {
            long now = System.nanoTime();
            double add = (now - b.lastRefillNanos) / 1e9 * refillPerSec;
            b.tokens = Math.min(capacity, b.tokens + add);
            b.lastRefillNanos = now;
            if (b.tokens >= 1) { b.tokens--; return true; }
            return false;
        }
    }
}
```

---

#### 4.11 Stack Overflow

**Requirements (real Amazon SDE-2 prompt, Jan 2025)**
- Post a question; answer a question; comment on either.
- Upvote / downvote.
- Search by tag / keyword.
- Reputation system (upvote = +10, accepted answer = +25).

**Core classes**
`User`, `Question`, `Answer`, `Comment`, `Vote`, `Tag`, `SearchService`.

**Patterns**
- **Composite** — `Votable` interface implemented by Question/Answer/Comment.
- **Observer** — author notified on new answer / accepted answer.
- **Strategy** — search ranking.

```java
interface Votable { void upvote(User u); void downvote(User u); int score(); }
abstract class Post implements Votable {
    User author; String body; Map<User, VoteType> votes = new ConcurrentHashMap<>();
    public void upvote(User u){ if (votes.put(u, VoteType.UP) != VoteType.UP) author.addReputation(10); }
    public int score(){ /* sum */ return 0; }
}
class Question extends Post { List<Answer> answers = new ArrayList<>(); Set<Tag> tags; Answer accepted; }
class Answer extends Post   { Question parent; }
```

---

#### 4.12 Tic Tac Toe

**Requirements**
- 3×3 board (or generalize to N×N with win-length k).
- Two players alternate; X always first.
- Detect win / draw; reject invalid moves; allow reset.

**Patterns**
- **State** — game state: `IN_PROGRESS / WON / DRAW`.
- **Strategy** — pluggable win-condition for N×N.

```java
class Game {
    char[][] board = new char[3][3];
    char current = 'X';
    GameStatus status = GameStatus.IN_PROGRESS;

    public synchronized boolean move(int r, int c) {
        if (status != GameStatus.IN_PROGRESS) return false;
        if (board[r][c] != 0) return false;
        board[r][c] = current;
        if (won(r, c)) status = (current == 'X') ? GameStatus.X_WON : GameStatus.O_WON;
        else if (full()) status = GameStatus.DRAW;
        else current = (current == 'X') ? 'O' : 'X';
        return true;
    }
    private boolean won(int r, int c) { /* check row, col, both diags */ return false; }
    private boolean full() { /* count moves */ return false; }
}
```

**Follow-ups**
- "Generalize to N×N with k-in-a-row." → store row/col/diag counters per player to keep `won()` O(1).
- "AI player." → introduce `Player` interface with `HumanPlayer` and `MinimaxPlayer`.

---

#### 4.13 Chess

**Requirements**
- 8×8 board, 6 piece types per side.
- Validate moves per piece, including capture.
- Check / checkmate / stalemate detection.
- Special moves: castling, en passant, promotion (often de-scoped at first).

**Patterns**
- **Factory** — create pieces.
- **Strategy / Template Method** — each piece has its own move-validation strategy.
- **State** — game state.

```java
abstract class Piece {
    Color color; boolean killed;
    abstract boolean canMove(Board b, Cell from, Cell to);
}
class Knight extends Piece {
    boolean canMove(Board b, Cell f, Cell t){
        int dr = Math.abs(f.row - t.row), dc = Math.abs(f.col - t.col);
        return dr * dc == 2 && (t.piece == null || t.piece.color != color);
    }
}
class Game {
    Board board; Player[] players; Player turn;
    boolean move(Player p, Cell from, Cell to){
        if (p != turn) return false;
        Piece pc = from.piece;
        if (pc == null || pc.color != p.color || !pc.canMove(board, from, to)) return false;
        if (to.piece != null) to.piece.killed = true;
        to.piece = pc; from.piece = null;
        turn = (turn == players[0]) ? players[1] : players[0];
        return true;
    }
}
```

---

#### 4.14 ATM

**Requirements**
- Card insertion + PIN auth.
- Operations: balance, withdraw, deposit, transfer.
- Cash dispenser holds notes of multiple denominations; minimize note count on withdrawal.
- Out-of-cash / out-of-paper states.

**Patterns**
- **State** — ATM: `IDLE / CARD_INSERTED / AUTHENTICATED / TRANSACTION_IN_PROGRESS / OUT_OF_SERVICE`.
- **Chain of Responsibility** — cash dispenser (₹2000 → ₹500 → ₹100).
- **Factory** — create transaction by type.

```java
abstract class CashDispenser { CashDispenser next;
    abstract void dispense(int amount);
}
class Dispenser2000 extends CashDispenser {
    int notes2k;
    void dispense(int amt){
        int use = Math.min(amt / 2000, notes2k);
        notes2k -= use; amt -= use * 2000;
        if (amt > 0 && next != null) next.dispense(amt);
        else if (amt > 0) throw new IllegalStateException("can't dispense exactly");
    }
}
```

---

#### 4.15 Snake and Ladder

**Requirements**
- N×N board (usually 10×10 = 100).
- K snakes, L ladders.
- Multiple players; dice 1–6; first to reach 100 wins.
- Roll-again on 6 (configurable).

**Patterns**
- **Singleton** — game.
- **Strategy** — dice (1-die vs 2-dice; biased dice).

```java
class Game {
    Map<Integer, Integer> jumps = new HashMap<>();  // start -> end (snake or ladder)
    Queue<Player> players;
    int boardSize = 100;
    Dice dice;

    Player play() {
        while (true) {
            Player p = players.poll();
            int roll = dice.roll();
            int next = p.position + roll;
            if (next > boardSize) { players.add(p); continue; }
            if (jumps.containsKey(next)) next = jumps.get(next);
            p.position = next;
            if (next == boardSize) return p;
            players.add(p);
        }
    }
}
```

---

### TIER 3 — Asked, less frequent (be ready to sketch in 30 min)

---

#### 4.16 Hotel Management / OYO

`Hotel`, `Room` (with `RoomType`, `RoomStatus`), `Reservation`, `Guest`, `Pricing`, `Search`. Patterns: Strategy (pricing, room-selection), State (reservation), Observer (housekeeping).

#### 4.17 Library Management

`Book`, `BookItem` (physical copy), `Member`, `Loan`, `Reservation`, `Fine`. Patterns: State (BookItem: AVAILABLE/LOANED/RESERVED/LOST), Strategy (fine calculation).

#### 4.18 Food Ordering (Swiggy / Zomato / DoorDash)

`Restaurant`, `MenuItem`, `Cart`, `Order`, `DeliveryPartner`, `PaymentService`, `OrderStatus` state machine: `PLACED → ACCEPTED → PREPARING → READY → PICKED_UP → DELIVERED / CANCELLED`. Patterns: State, Observer (push status to user), Strategy (assign delivery partner).

#### 4.19 Online Shopping Cart (Amazon-style)

`Product`, `Cart`, `CartItem`, `Order`, `Inventory`, `Discount`, `PaymentMethod`. Patterns: Strategy (discount, shipping, payment), Decorator (gift wrap), Observer (inventory alerts). Watch concurrency on `Inventory.reserve()`.

#### 4.20 Ride-sharing (Uber)

`Rider`, `Driver`, `Trip`, `Location`, `Matcher`, `Fare`, `TripStatus`. Patterns: Strategy (matching: nearest, surge-aware), Observer (location updates), State (trip).

#### 4.21 Music Streaming (Spotify)

`User`, `Song`, `Album`, `Artist`, `Playlist`, `Subscription`, `Player` (state machine: PLAYING/PAUSED/STOPPED), `RecommendationStrategy`.

#### 4.22 Meeting Room Scheduler / Reservation

Asked as both LLD and DSA (`Meeting Rooms III`). Classes: `Room`, `Booking`, `Calendar`, `BookingService`. Patterns: Strategy (room-pick: smallest-that-fits, capacity-aware), TreeMap of `(startTime → booking)` for O(log n) conflict check.

#### 4.23 URL Shortener (TinyURL)

`UrlService`, `ShortCodeGenerator` (base62 from auto-id, or hash-and-collision-resolve), `UrlMapping`, `AnalyticsService`. Patterns: Strategy (generation), Singleton, Observer (analytics).

#### 4.24 In-memory File System

`Node` (abstract), `File`, `Directory` (composite). Operations: `mkdir`, `ls`, `addContent`, `readContent`, `find`. Patterns: **Composite** is the canonical example.

#### 4.25 Customer-Support Ticketing

`Customer`, `Agent`, `Ticket`, `TicketStatus` (OPEN/ASSIGNED/IN_PROGRESS/RESOLVED/CLOSED), `AssignmentStrategy` (round-robin, least-loaded, skill-based). Patterns: Strategy (assignment), Observer (updates), State (ticket lifecycle), Chain of Responsibility (escalation).

---

## 5) Concurrency / multithreading add-ons Amazon loves to ask

Whenever your design touches a shared resource (a parking spot, a seat, a locker, an inventory row, a cache entry), expect a follow-up like *"two requests come in at the same time — what happens?"* Be ready with:

- **CAS / `AtomicReference`** for single-cell ownership (parking spot, locker).
- **`ConcurrentHashMap` + `computeIfAbsent`** for keyed state (seat locks, rate-limit buckets).
- **`ReentrantLock` / `ReadWriteLock`** for multi-step critical sections (booking flow).
- **`BlockingQueue` + producer/consumer** for pipelines (elevator request queue, logger async append, notification dispatch).
- **`ScheduledExecutorService`** for TTL sweeps (seat locks, lockers, cache expiry).
- **Idempotency keys** for retries (orders, payments).

Practice writing 2-3 of these from scratch:
- `BlockingQueue<T>` with `ReentrantLock + Condition`.
- Thread-safe singleton with double-checked locking + `volatile`.
- Producer/consumer with `wait`/`notify`.

---

## 6) Behavioral wrapping — LP signals interviewers look for in LLD rounds

Even in a "technical" LLD round, Amazon interviewers grade Leadership Principles in your behavior:

- **Customer Obsession** — when clarifying requirements, frame them from the user's perspective ("a user dropping off a package would want…").
- **Are Right, A Lot** — when challenged on a design choice, defend it with reasons, but back down quickly if the interviewer's point is stronger. Real rejections often cite "couldn't justify trade-offs."
- **Dive Deep** — if asked "how does that work under contention," go into atomicity, memory model, etc.
- **Bias for Action** — start writing code by the ~15-min mark; perfect-but-late designs are penalized.
- **Insist on the Highest Standards** — voluntarily mention edge cases, validation, thread safety.
- **Invent and Simplify** — don't pile on patterns; if a `Map<>` works, say so.

---

## 7) 4-week study plan + resources

### Week 1 — Foundations
- OOP review: inheritance vs composition; SOLID with examples.
- Patterns: Strategy, Observer, Factory, Singleton (write each from scratch once).
- Practice problems: **Parking Lot**, **Vending Machine**, **Tic Tac Toe**.

### Week 2 — Booking / state-machine systems
- Patterns: State, Decorator.
- Practice problems: **BookMyShow**, **Elevator**, **Amazon Locker**, **ATM**.
- Daily: 1 problem, 60 min, write runnable code with a `main` driver.

### Week 3 — Concurrency-heavy & service-style
- Concurrency primitives, thread-safe singleton, blocking queue.
- Patterns: Chain of Responsibility, Builder, Composite.
- Practice problems: **LRU Cache (thread-safe)**, **Rate Limiter**, **Logger**, **Notification Service**, **Stack Overflow**.

### Week 4 — Mocks & breadth
- 1 mock interview / day (45 min) — record yourself.
- Cover the Tier-3 list at sketch level (you should be able to draw the class diagram and name the patterns in 5 min).
- Re-do Tier-1 problems from a blank file in 35 min.

### High-signal resources
- **GitHub: `ashishps1/awesome-low-level-design`** — free, problem-by-problem repo with Java code.
- **GitHub: `prasadgujar/low-level-design-primer`** — curated problem list with solution links.
- **Concept && Coding (Shrayansh Jain)** — YouTube playlist on LLD, widely recommended in Amazon SDE-2 acceptance write-ups.
- **Hello Interview — "How to prepare for LLD"** — modern framework, lighter on UML.
- **AlgoMaster.io / lowleveldesignmastery.com** — practice problems with company tags ("Amazon").
- **Concurrency in Practice (Brian Goetz)** — first 5 chapters for the multithreaded follow-ups.

### Cadence on the interview day
- Spend 5–6 min on requirements. Resist the urge to start coding.
- Whiteboard the class diagram (just boxes + relations) at minute 10.
- Start coding at minute 12–15.
- At minute 35, pause to verbalize: thread safety, extensibility, failure modes.
- Leave 5 min for the interviewer's follow-ups.

---

## Final checklist (print and tick off)

- [ ] I can solve Parking Lot in 35 min, with thread safety and a pluggable strategy.
- [ ] I can write a thread-safe LRU from scratch, no peeking.
- [ ] I can explain (and write) seat-locking for BookMyShow.
- [ ] I can name the 6 patterns above and give one Amazon example for each.
- [ ] I have a STAR story for Customer Obsession, Dive Deep, Bias for Action, Ownership, and Are Right A Lot — each <2 min.
- [ ] I've done at least 2 mock interviews.

Good luck. The LLD round rewards calm, structured thinking more than memorized solutions — practice the 6-step framework on every problem above, and you'll be ready.