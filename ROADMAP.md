# oxyMP - Development RoadMap

## Phase 0: Platform Abstraction Layer (Этапы 1-15)

### Этап 1: Project Structure & Build System
- Создание монорепозитория с модульной архитектурой
- CMake 3.20+ для C++ (multi-config generators)
- Cargo workspace для Rust компонентов
- CI/CD pipeline (GitHub Actions)
- Code coverage setup (lcov/gcov)
- Static analysis (clang-tidy, cppcheck)

### Этап 2: Platform - Core Detection
- Platform detection (WIN32, LINUX, MACOS, BSD)
- Architecture detection (x86, x64, ARM, ARM64)
- Compiler detection (MSVC, GCC, Clang)
- Feature detection (SSE, AVX, NEON)
- Build configuration (Debug, Release, RelWithDebInfo)

### Этап 3: Platform - Type System
- Fixed-width integers (int8-int64, uint8-uint64)
- Floating point (float32, float64)
- Platform size types (size_t, ptrdiff_t wrappers)
- Character types (char8_t, char16_t, char32_t)
- Boolean standardization

### Этап 4: Platform - Memory API
- Memory alignment (align, alignof)
- Cache line size detection
- Memory barriers (acquire, release, seq_cst)
- Prefetch hints
- SIMD alignment macros
- Page size detection

### Этап 5: Platform - Memory Allocators
- System allocator wrapper (malloc/free с tracking)
- Pool allocator (fixed-size blocks)
- Stack/Linear allocator (bump allocation)
- Arena allocator (region-based)
- Thread-local allocators
- Memory leak detection
- Allocation statistics

### Этап 6: Platform - Threading API
- Thread creation/destruction
- Thread naming (SetThreadDescription)
- CPU affinity (thread pinning)
- Thread priority control
- Thread-local storage (TLS)
- Hardware concurrency detection
- Thread pool foundation

### Этап 7: Platform - Synchronization Primitives
- Mutex (critical section/pthread_mutex)
- Recursive mutex
- Spinlock (atomic flag)
- Reader-writer lock
- Semaphore
- Condition variable
- Event/Barrier

### Этап 8: Platform - Atomic Operations
- Atomic types wrapper (int32, int64, ptr)
- Compare-and-swap (CAS)
- Fetch-and-add/sub/and/or/xor
- Exchange and load/store
- Memory ordering control
- Lock-free counter

### Этап 9: Platform - FileSystem API
- File handle wrapper (RAII)
- Open/close/read/write/seek
- File size and attributes
- Directory creation/removal
- Directory iteration
- Path manipulation (join, normalize, absolute)
- File permissions and timestamps

### Этап 10: Platform - Virtual FileSystem (VFS)
- VFS interface и mount points
- Physical filesystem backend
- Archive backend (ZIP support via miniz)
- Memory filesystem backend
- Layered/overlay filesystems
- File watching (inotify/ReadDirectoryChangesW)
- Async I/O support

### Этап 11: Platform - Time API
- High-resolution timer (QueryPerformanceCounter/clock_gettime)
- System time (UTC, local)
- Monotonic clock
- Timestamp conversion
- Sleep/yield functions
- Timer wheel for callbacks
- Performance counter utilities

### Этап 12: Platform - Process API
- Process spawning (CreateProcess/fork+exec)
- Process termination and wait
- Environment variables (get/set)
- Command line argument parsing
- Working directory operations
- Process ID and parent ID
- Standard I/O redirection

### Этап 13: Platform - Dynamic Library Loader
- Library loading (LoadLibrary/dlopen)
- Symbol resolution (GetProcAddress/dlsym)
- Library unloading
- Error reporting
- Module enumeration
- Dependency walking

### Этап 14: Platform - Console API
- Console output (stdout/stderr)
- ANSI color codes support
- Console input (blocking/non-blocking)
- Clear screen and cursor control
- Console window title
- Virtual terminal sequences

### Этап 15: Platform - Debug Utilities
- Assert with message
- Debug break (DebugBreak/__builtin_trap)
- Stack trace capture (StackWalk64/backtrace)
- Symbol resolution (DbgHelp/addr2line)
- Minidump generation
- Debug string output

---

## Phase 1: Core Foundation (Этапы 16-40)

### Этап 16: Shared - Math Library
- Vector2/3/4 (SIMD optimized)
- Matrix3x3, Matrix4x4
- Quaternion (slerp, squad)
- Transform (TRS decomposition)
- AABB, OBB, Sphere, Capsule
- Ray, Plane, Frustum
- Intersection tests
- Math utilities (lerp, smoothstep, etc.)

### Этап 17: Shared - String Library
- String view (non-owning)
- Dynamic string (COW - Copy-on-Write)
- String builder
- UTF-8/16/32 encoding/decoding
- String hashing (FNV-1a, xxHash, CRC32)
- Format string (printf-like)
- String interning/pool

### Этап 18: Shared - Container Library
- Dynamic array (std::vector-like)
- Small vector optimization
- Hash map (Robin Hood hashing)
- Hash set
- Intrusive linked list
- Ring buffer (lock-free variant)
- Sparse set (ECS-optimized)
- Bitset and bit array

### Этап 19: Shared - Smart Pointers
- Unique pointer (unique ownership)
- Shared pointer (reference counted)
- Weak pointer
- Intrusive pointer
- Handle system (generational indices)
- Object pool with handles

### Этап 20: Shared - GUID System
- UUID v4 generation
- GUID from string
- GUID comparison and hashing
- Network byte order conversion
- Null GUID constant

### Этап 21: Logging System
- spdlog integration
- Multi-sink support (console, file, network)
- Log levels (trace, debug, info, warn, error, critical)
- Structured logging (JSON format)
- Log rotation and compression
- Thread-safe async logging
- Performance monitoring hooks

### Этап 22: Configuration System
- JSON parser (nlohmann/json или simdjson)
- YAML support (yaml-cpp)
- TOML support
- Hot-reload mechanism
- Environment variable expansion
- Schema validation
- Hierarchical configs (inheritance)

### Этап 23: Event System - Core
- Event dispatcher (type-safe)
- Event queue (priority queue)
- Immediate vs deferred events
- Event filtering
- Event cancellation
- Subscriber management
- Thread-safe event bus

### Этап 24: Event System - Advanced
- Event recording/replay
- Event batching
- Event compression
- Network event sync
- Event serialization
- Performance metrics

### Этап 25: Error Handling Framework
- Error code enumeration
- Result<T, Error> type
- Exception hierarchy
- Error context (stack trace, file/line)
- Error recovery strategies
- Error reporting system
- Error localization

### Этап 26: Job System - Foundation
- Thread pool implementation
- Work-stealing queue
- Job priorities
- Job dependencies (task graph)
- Job cancellation
- CPU affinity per worker
- Job statistics

### Этап 27: Job System - Advanced
- Fiber-based jobs (context switching)
- Async/await pattern
- Parallel-for utilities
- Pipeline jobs
- Job profiling
- Job visualization tools
- Background job queue

### Этап 28: Reflection System - Core
- Type registry
- Type information (name, size, alignment)
- Field/property registration
- Method registration
- Enum reflection
- Inheritance information
- Attribute/annotation system

### Этап 29: Reflection System - Serialization
- Generic serializer interface
- JSON serialization
- Binary serialization (FlatBuffers)
- MessagePack serialization
- Versioning support
- Custom serializer support
- Polymorphic serialization

### Этап 30: Reflection System - Utilities
- Object cloning
- Object comparison
- Property iteration
- Method invocation
- Factory registration
- Inspector/editor support
- Documentation generation

### Этап 31: Network Library - Core (Rust)
- QUIC setup (quinn)
- Connection state machine
- Connection pooling
- Endpoint management
- Certificate handling (rustls)
- Connection migration
- 0-RTT support

### Этап 32: Network Library - Reliability
- Packet acknowledgment
- Automatic retransmission
- Ordering guarantees
- Duplicate detection
- Out-of-order handling
- Fragment reassembly
- Flow control

### Этап 33: Network Library - Serialization
- FlatBuffers schema definition
- Packet structure (header, payload)
- Compression (LZ4, Zstd)
- Encryption (ChaCha20-Poly1305)
- Delta encoding
- Bit packing utilities
- Custom serializers

### Этап 34: Network Library - Bandwidth Management
- Rate limiting (token bucket)
- Priority queues (high/medium/low)
- Congestion control (BBR-like)
- Bandwidth estimation
- QoS policies
- Metrics collection (latency, packet loss)
- Network simulator (artificial lag/loss)

### Этап 35: Network Library - C++ Bindings
- FFI interface (extern "C")
- RAII wrappers
- Connection handle
- Async callback system
- Error propagation
- Thread-safe API
- Smart pointer integration

### Этап 36: Database Abstraction Layer
- Connection interface
- Connection pooling
- Prepared statements
- Transaction support (BEGIN, COMMIT, ROLLBACK)
- Query builder
- Result set iteration
- Async queries

### Этап 37: PostgreSQL Integration
- libpq wrapper
- Type mapping (C++ <-> SQL)
- Array and JSON support
- LISTEN/NOTIFY
- Connection string parsing
- SSL support
- Migration system

### Этап 38: Redis Integration
- hiredis wrapper
- Pub/Sub support
- Pipelining
- Transactions (MULTI/EXEC)
- Lua script execution
- Cluster support
- Session storage

### Этап 39: Security Module - Cryptography
- Key exchange (X25519, ECDH)
- Encryption (ChaCha20, AES-GCM)
- AEAD (Authenticated Encryption)
- Hash functions (SHA-256, BLAKE3)
- HMAC implementation
- Secure random (OS crypto API)
- Key derivation (PBKDF2, Argon2)

### Этап 40: Security Module - Authentication
- JWT token generation/validation
- Password hashing (Argon2id)
- Rate limiting (token bucket per IP)
- Anti-replay (nonce tracking)
- Session management
- 2FA support (TOTP)
- API key generation

---

## Phase 2: Reverse Engineering Framework (Этапы 41-55)

### Этап 41: RE Framework - Core Architecture
- Module interface definition
- Version abstraction layer
- Game build detection
- Hooking policy interface
- Memory safety guards
- Error recovery system
- Isolation from game logic

### Этап 42: RE Framework - Pattern Scanner
- Boyer-Moore algorithm
- Wildcard support (? for any byte)
- Multi-pattern scanning
- Signature database (JSON/YAML)
- Cache mechanism
- Parallel scanning
- Scan result validation

### Этап 43: RE Framework - Memory Manager
- Process memory reader/writer
- Memory protection (VirtualProtect)
- Memory allocation in remote process
- Pattern matching in memory
- Pointer chain resolution
- Memory patch system
- Rollback/restore capabilities

### Этап 44: RE Framework - Hook Manager
- MinHook integration
- Hook registration interface
- Detour/trampoline management
- Hook enable/disable
- Hook chain support
- VTable hooking
- IAT/EAT hooking

### Этап 45: RE Framework - Native Function System
- Native hash database (YAML/JSON)
- Native call interface (x64 calling convention)
- Return value handling
- Argument marshalling (types)
- Native context (scrProgram/scrThread)
- Native queue system
- Native result caching

### Этап 46: RE Framework - Address Database
- Game version fingerprinting
- Offset database (per version)
- Address resolver
- Auto-update mechanism
- Fallback to pattern scanning
- Version compatibility matrix
- Offset generator tool

### Étap 47: RE Framework - Game Version Manager
- Build number detection
- Executable hash verification
- Version string parsing
- Steam/Epic/Rockstar detection
- DLC detection
- Update notification
- Migration paths

### Этап 48: RE Framework - Crash Handler
- SEH (Structured Exception Handling)
- Vectored exception handler
- Stack unwinding
- Minidump generation with context
- Crash report submission
- Exception filtering
- Graceful degradation

### Этап 49: RE Framework - Symbol Loader
- PDB parsing (if available)
- Symbol resolution
- Function name lookup
- Type information extraction
- Debug info caching
- Third-party symbol support

### Этап 50: RE Framework - Script Hook
- ScriptThread management
- Script registration
- Script lifecycle
- Fiber integration
- Script yielding
- Script termination
- Script isolation

### Этап 51: RE Framework - Game Structs
- CPlayerInfo structure
- CPed structure
- CVehicle structure
- CObject structure
- CWorld interfaces
- CStreaming interfaces
- Game state wrappers

### Этап 52: RE Framework - Patch Manager
- Patch definition format
- Runtime patching
- NOP instructions
- Jump/call redirection
- Patch versioning
- Conflict detection
- Automatic rollback

### Этап 53: RE Framework - Testing Utilities
- Unit tests for pattern scanner
- Hook validation tests
- Native call tests
- Memory safety tests
- Version compatibility tests
- Regression test suite

### Этап 54: RE Framework - Documentation
- Architecture documentation
- API reference (Doxygen)
- Pattern database format
- Hook safety guidelines
- Memory layout diagrams
- Version porting guide

### Этап 55: RE Framework - Public API
- Clean C++ interface
- Version-agnostic API
- Feature detection
- Error codes
- Initialization/shutdown
- Configuration interface
- Callback system

---

## Phase 3: Code Generation & Tooling (Этапы 56-70)

### Этап 56: Code Generator - Foundation
- Abstract syntax tree (AST)
- Template engine
- Code formatting (clang-format integration)
- Multi-file generation
- Incremental builds
- Dependency tracking

### Этап 57: Reflection Generator
- C++ parsing (libclang)
- Annotation/attribute parsing
- Type extraction
- Generate reflection registration code
- Header generation
- Integration with build system

### Этап 58: Native Generator
- Native definition parser
- Native hash database updater
- Generate native invoke code
- Generate native documentation
- Type-safe wrapper generation
- Lua/JS bindings

### Этап 59: Protocol Generator
- FlatBuffers schema generation from reflection
- Packet ID auto-assignment
- RPC stub generation (client/server)
- Serialization code
- Validation code
- Version compatibility

### Этап 60: Packet Generator
- Network packet definition DSL
- Packet class generation
- Packet handler registration
- Packet documentation
- Packet test generation
- Network protocol documentation

### Этап 61: SDK Generator
- Public API header extraction
- Documentation generation
- Example code generation
- Project template generation
- CMake config generation
- Package creation

### Этап 62: Resource Manifest Generator
- Resource.json schema
- Dependency resolution code
- Asset reference validation
- Entry point generation
- Metadata extraction
- Hot-reload support code

### Этап 63: Documentation Generator
- Markdown documentation from code
- API reference (HTML)
- Diagram generation (PlantUML)
- Tutorial generation
- Changelog generation
- Cross-reference linking

### Этап 64: Code Templates
- Project scaffolding templates
- Component templates
- System templates
- Resource templates
- Plugin templates
- Test templates

### Этап 65: Build Automation
- CMake generator improvements
- Dependency fetching (vcpkg/conan)
- Parallel build optimization
- Precompiled headers
- Unity builds (optional)
- Build time tracking

### Этап 66: Developer Tools - CLI
- Command-line tool framework
- Resource compiler CLI
- Asset importer CLI
- Native database updater CLI
- Code generator CLI
- Server admin CLI

### Этап 67: Developer Tools - Profiler
- CPU profiler (Tracy integration)
- Memory profiler
- Network profiler
- Job system profiler
- Frame timeline
- Flame graphs

### Этап 68: Developer Tools - Debugger
- Entity inspector
- Network packet inspector
- Memory inspector
- Event log viewer
- Script debugger interface
- Live variable watch

### Этап 69: Developer Tools - Live Console
- In-game console (ImGui)
- Command registration
- Autocomplete
- Command history
- Variable inspection
- Expression evaluation

### Этап 70: Developer Tools - Debug Overlay
- FPS counter
- Network stats (ping, packet loss)
- Entity count
- Memory usage
- Job system status
- Custom metrics display

---

## Phase 4: Replication Framework (Этапы 71-85)

### Этап 71: Replication - Architecture
- Replication graph interface
- Replicable object base class
- Replication policy (ownership, frequency)
- Priority system
- Interest management
- Replication channels
- Component-based replication

### Этап 72: Replication - Snapshot System
- Snapshot structure
- Snapshot creation
- Snapshot comparison
- Snapshot storage
- Snapshot history (circular buffer)
- Snapshot compression
- Snapshot validation

### Этап 73: Replication - Delta Compression
- Delta calculation (XOR, binary diff)
- Delta encoding
- Delta application
- Bitpacking optimization
- Quantization (position, rotation)
- Lossy compression (acceptable error)
- Delta prioritization

### Этап 74: Replication - State Buffer
- Ring buffer for states
- State interpolation
- State extrapolation
- Jitter buffer
- Out-of-order handling
- Gap detection
- Rewind support

### Этап 75: Replication - Entity Ownership
- Authority transfer
- Ownership policies (server, client)
- Autonomous proxy
- Simulated proxy
- Ownership handoff
- Conflict resolution

### Этап 76: Replication - Interest Management
- Spatial partitioning (grid, octree)
- Distance-based culling
- View frustum culling
- Interest radius
- Dynamic priority
- Subscription system
- Update frequency scaling

### Этап 77: Replication - Prediction
- Client-side prediction
- Input buffering
- Predicted state
- Server reconciliation
- Rollback mechanism
- Prediction error correction
- Prediction validation

### Этап 78: Replication - Interpolation
- Linear interpolation
- Hermite interpolation
- Rotation slerp
- Velocity-based extrapolation
- Adaptive buffering
- Smoothing algorithms
- Teleport detection

### Этап 79: Replication - Rollback Support
- State history management
- Deterministic simulation
- Replay input
- State restoration
- Collision recomputation
- Physics rollback
- Event replay

### Этап 80: Replication - Property Replication
- Property change tracking
- Dirty flag system
- Reliable properties
- Unreliable properties
- Property groups
- Conditional replication
- RPC integration

### Этап 81: Replication - Optimizations
- Relevancy filtering
- Update aggregation
- Bandwidth budgeting
- Adaptive update rates
- Spatial hashing
- Level-of-detail (LoD)
- Multicast groups

### Этап 82: Replication - Debug Tools
- Replication visualizer
- Packet inspector
- Snapshot diff viewer
- Prediction error display
- Bandwidth monitor
- Entity replication status
- Network simulator integration

### Этап 83: Replication - Testing
- Unit tests for delta compression
- Snapshot consistency tests
- Prediction accuracy tests
- Interpolation tests
- Stress tests (1000+ entities)
- Network condition simulation
- Regression test suite

### Этап 84: Replication - Documentation
- Architecture overview
- Component guide
- Best practices
- Performance tuning
- Troubleshooting guide
- API reference

### Этап 85: Replication - Example Implementations
- Player replication example
- Vehicle replication example
- Object replication example
- Weapon replication example
- Reference implementations

---

## Phase 5: Client Foundation (Этапы 86-110)

### Этап 86: Client - Project Setup
- CMake configuration
- Module dependencies
- DLL project setup
- Export definitions
- Build configurations
- Testing framework

### Этап 87: Client - DLL Injection
- Process injection (CreateRemoteThread)
- Manual mapping
- Thread hijacking
- Stealth injection
- Anti-detection measures
- Error handling
- Injection verification

### Этап 88: Client - Initialization
- RE Framework initialization
- Game version detection
- Hook installation
- Memory allocation
- Event system setup
- Configuration loading
- Graceful failure

### Этап 89: Client - Game Integration
- DllMain entry point
- Game state detection
- Loading screen handling
- Menu detection
- Session lifecycle
- Cleanup on disconnect
- Crash recovery

### Этап 90: Client - Entity System Base
- Entity base class
- Entity ID management (networked)
- Entity factory
- Entity lifecycle (create/destroy)
- Entity registry
- Entity queries
- Handle system

### Этап 91: Client - Local Player
- Local player wrapper
- Native function integration
- Player control state
- Camera management
- Input capture
- Health/armor
- Weapon management

### Этап 92: Client - Remote Player Entities
- Remote player class
- Ped handle management
- Model loading
- Appearance sync
- Animation state
- Name tag attachment
- Blip management

### Этап 93: Client - Vehicle Entities
- Vehicle base class
- Vehicle spawning
- Model streaming
- Mod synchronization
- Color sync
- License plate
- Occupant tracking

### Этап 94: Client - Object Entities
- Object spawning
- Dynamic objects
- Static objects
- Physics objects
- Parented objects
- Collision handling
- Texture dictionary loading

### Этап 95: Client - Network Client
- Connection to server
- Authentication handshake
- Packet handler registry
- Reconnection logic
- Timeout handling
- Latency tracking
- Connection quality monitoring

### Этап 96: Client - Player Synchronization
- Position/rotation replication
- Velocity/acceleration
- Animation sync
- Movement state (walking, running, etc.)
- Ragdoll sync
- Interpolation/extrapolation
- Teleport detection

### Этап 97: Client - Vehicle Synchronization
- Vehicle physics sync
- Wheel rotation/suspension
- Engine state
- Damage sync
- Passenger sync
- Trailer sync
- Collision reconciliation

### Этап 98: Client - Weapon Synchronization
- Weapon switching
- Ammo synchronization
- Shooting events (muzzle flash, tracer)
- Projectile sync (rockets, grenades)
- Hit detection (client-side with server validation)
- Recoil and spread
- Reload events

### Этап 99: Client - Animation System
- Animation dictionary loading
- Animation playback sync
- Blend tree support
- IK (Inverse Kinematics) adjustments
- Facial animations
- Gesture system
- Animation events

### Этап 100: Client - Streaming System
- Entity streaming (distance-based)
- LOD management
- Priority calculation
- Stream in/out events
- Model preloading
- Texture streaming
- Memory budget management

### Этап 101: Client - UI System - CEF Setup
- CEF initialization
- Browser process management
- Render handler (off-screen rendering)
- Texture update pipeline
- Input routing (keyboard/mouse)
- JavaScript <-> C++ bridge
- Resource protocol handler

### Этап 102: Client - UI System - JavaScript API
- Event system binding
- Native function binding
- Resource API exposure
- Player API
- Vehicle API
- UI focus management
- Cursor visibility

### Этап 103: Client - Input Manager
- Keyboard input capture
- Mouse input (delta, absolute)
- Controller support (XInput)
- Input blocking (for UI)
- Key binding system
- Input state tracking
- Input recording

### Этап 104: Client - Voice Chat Client
- Opus codec integration
- Audio capture (microphone)
- Audio playback (3D positioning)
- Voice activation detection
- Push-to-talk
- Volume control (per player)
- Voice indicators (UI)

### Этап 105: Client - Nametags System
- Player nametag rendering
- Distance culling
- Occlusion checking (raycasting)
- Custom styling (health bar, name)
- Scaling with distance
- Visibility toggling

### Этап 106: Client - Minimap & Blips
- Blip creation/destruction
- Blip types (player, waypoint, etc.)
- Route drawing
- GPS integration
- Blip color/sprite
- Minimap zoom

### Этап 107: Client - Chat System
- Chat message rendering
- Message history
- Chat commands
- Emoji support
- Spam protection
- Chat channels (global, local, team)
- Timestamp display

### Этап 108: Client - HUD System
- Custom HUD elements
- Native HUD control
- HUD components (health, armor, money)
- Responsive layout
- HUD hiding
- Custom textures

### Этап 109: Client - Notification System
- Native notifications
- Custom notifications
- Priority queue
- Animation (slide in/out)
- Icon support
- Stacking/grouping

### Этап 110: Client - Camera System
- Camera control (scripted cameras)
- Smooth camera transitions
- Cinematic mode
- First-person camera sync
- Camera shake
- Field of view control

---

## Phase 6: Server Foundation (Этапы 111-145)

### Этап 111: Server - Project Setup
- CMake configuration
- Executable setup
- Module linking
- Configuration files
- Daemon mode (Linux)
- Service installation (Windows)

### Этап 112: Server - Initialization
- Command-line argument parsing
- Configuration loading
- Database connection
- Network server startup
- Plugin loading
- Signal handling (SIGTERM, SIGINT)

### Этап 113: Server - Network Server
- QUIC server setup (via Rust FFI)
- Client connection handling
- Connection limits
- IP whitelist/blacklist
- DDoS protection (rate limiting)
- Geographic filtering

### Этап 114: Server - Client Manager
- Client connection tracking
- Authentication flow
- Session management
- Client state (connecting, connected, disconnected)
- Kick/ban system
- Timeout detection

### Этап 115: Server - Entity System - ECS Core
- Entity component system (EnTT или собственный)
- Component registry
- System scheduler
- Entity archetypes
- Component storage
- Entity queries

### Этап 116: Server - Entity System - Player Component
- Player component (name, health, position, etc.)
- Player spawn system
- Player death system
- Player respawn system
- Player state management
- Player permissions

### Этап 117: Server - Entity System - Vehicle Component
- Vehicle component
- Vehicle spawning system
- Vehicle ownership
- Vehicle respawn
- Vehicle persistence
- Vehicle locking

### Этап 118: Server - Entity System - Object Component
- Object component
- Object spawning
- Object lifecycle
- Parenting system
- Object pooling
- Object persistence

### Этап 119: Server - World Manager
- World state (time, weather)
- Time synchronization
- Weather transitions
- Traffic density
- Interior management
- World bounds

### Этап 120: Server - Streaming System
- Spatial partitioning (grid или octree)
- Per-player streaming
- Stream range calculation
- Network culling
- Entity visibility
- Streaming events

### Этап 121: Server - Event System
- Server event dispatcher
- Event priority
- Event cancellation
- Event propagation (to scripts)
- Built-in events (playerConnect, vehicleSpawn, etc.)
- Custom events

### Этап 122: Server - RPC System
- RPC registration
- Client->Server RPC
- Server->Client RPC
- Server->AllClients RPC
- RPC validation (authorization)
- RPC rate limiting

### Этап 123: Server - Replication Integration
- Entity replication setup
- Player replication
- Vehicle replication
- Object replication
- Snapshot generation
- Delta compression
- Priority management

### Этап 124: Server - Resource Manager
- Resource loading (filesystem)
- Resource metadata parsing
- Dependency injection
- Resource lifecycle (start/stop/restart)
- Resource isolation (separate V8 context)
- Resource versioning

### Этап 125: Server - Script Runtime - V8 Setup
- V8 initialization
- Isolate management
- Context creation per resource
- Module loading (ES6)
- Garbage collection tuning
- Memory limits

### Этап 126: Server - Script Runtime - Native Bindings
- C++ to JS binding (v8pp или собственный)
- Class wrapping
- Method export
- Property accessors
- Callback handling
- Promise support

### Этап 127: Server - Script Runtime - Core API
- Console API (log, warn, error)
- Timers (setTimeout, setInterval)
- Event API (on, off, emit)
- Resource API (getResource, startResource)
- Export/import between resources

### Этап 128: Server - Script Runtime - Player API
- Player class binding
- Player properties (name, health, position)
- Player methods (kick, ban, sendMessage)
- Player events (onConnect, onDisconnect)
- Player data storage

### Этап 129: Server - Script Runtime - Vehicle API
- Vehicle class binding
- Vehicle creation
- Vehicle properties (model, color, position)
- Vehicle methods (repair, explode)
- Vehicle events

### Этап 130: Server - Script Runtime - Entity API
- Entity base class
- Entity creation/destruction
- Entity properties
- Entity methods
- Entity events
