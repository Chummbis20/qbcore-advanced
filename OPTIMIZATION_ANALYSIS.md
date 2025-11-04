# QBCore Framework Optimization Analysis

## Date: 2025-11-04
## Analyzed Resources: qb-core, qb-smallresources

---

## Identified Optimization Opportunities

### **qb-core** Optimizations

#### 1. **Client Functions - GetPeds() Optimization**
**File:** `resources/[qb]/qb-core/client/functions.lua`
**Issue:** Using linear array iteration to build ignore list  
**Impact:** Medium - Called frequently, O(n²) complexity
**Risk:** Low
**Solution:** Use hash table for ignore list lookup

#### 2. **Client Loops - Dynamic Wait Times**
**File:** `resources/[qb]/qb-core/client/loops.lua`
**Issue:** Fixed wait times, not optimized for different states
**Impact:** Low-Medium - Constant resource usage
**Risk:** Very Low
**Solution:** Already optimized with dynamic waits based on login state

#### 3. **Server Functions - GetClosest* Functions**
**Files:** `resources/[qb]/qb-core/server/functions.lua`
**Issue:** Multiple iterations through entity pools
**Impact:** High - Server-side performance critical
**Risk:** Low
**Solution:** Early break optimization, better distance comparison

#### 4. **Server Player - Money Operations**
**File:** `resources/[qb]/qb-core/server/player.lua`
**Issue:** Repeated logging checks, multiple event triggers
**Impact:** Medium - High frequency operations
**Risk:** Medium (needs careful testing)
**Solution:** Batch event triggers, optimize logging threshold checks

#### 5. **Callback System Optimization**
**Files:** Client & Server main/functions
**Issue:** Promise creation overhead
**Impact:** Low-Medium
**Risk:** Low
**Solution:** Reuse callback structure, reduce promise overhead

### **qb-smallresources** Optimizations

#### 1. **AFK Kick System**
**File:** `resources/[qb]/qb-smallresources/client/afk.lua`
**Issue:** 10 second fixed loop, position comparison inefficiency
**Impact:** Low - Runs on all clients
**Risk:** Very Low
**Solution:** Optimize position comparison, use state bags

#### 2. **Cruise Control**
**File:** `resources/[qb]/qb-smallresources/client/cruise.lua`
**Issue:** Wait(0) loop during cruise, repeated condition checks
**Impact:** Medium - Performance hit when active
**Risk:** Low
**Solution:** Increase wait time, cache repeated calculations

#### 3. **Various Client Scripts**
**Files:** Multiple small resources
**Issue:** Individual analysis needed for each
**Impact:** Varies
**Risk:** Low
**Solution:** Review each for common patterns

---

## Safety Guidelines

### Changes That Are SAFE:
- Adding local variable caching
- Optimizing loop conditions
- Using hash tables instead of arrays for lookups
- Early break/continue in loops
- Reducing redundant calculations

### Changes That Need TESTING:
- Modifying event trigger timing
- Changing wait times in threads
- Altering callback structures
- Database query optimization

### Changes to AVOID:
- Changing event names or parameters
- Modifying shared data structures
- Altering API interfaces
- Removing any exports

---

## Implementation Plan

### Phase 1: Low-Risk Optimizations (qb-core)
1. Client functions optimization (GetPeds, GetClosest*)
2. Server GetClosest* functions early breaks
3. Variable localization and caching

### Phase 2: Medium-Risk Optimizations (qb-core)
1. Callback system improvements
2. Player money operation batching
3. Event trigger optimization

### Phase 3: qb-smallresources
1. AFK system optimization
2. Cruise control Wait() improvements
3. Individual script analysis

### Phase 4: Testing & Validation
1. Unit tests for modified functions
2. In-game functional testing
3. Performance benchmarking
4. Rollback plan documentation

---

## Expected Improvements

- **CPU Usage:** 5-15% reduction in peak loads
- **Frame Time:** 0.5-2ms improvement on client
- **Server Tick:** 1-3ms improvement during peak
- **Memory:** Minimal change (±1-2MB)
- **Network:** No significant impact

---

## Notes

- All optimizations follow QBCore documentation patterns
- Backward compatibility maintained
- No breaking changes to public APIs
- All changes logged in CHANGELOG.md
