# QBCore Optimization Testing Guide

## Pre-Deployment Checklist

### 1. Backup Current Installation
```bash
# Create backup of modified resources
cp -r resources/[qb]/qb-core resources/[qb]/qb-core.backup
cp -r resources/[qb]/qb-smallresources resources/[qb]/qb-smallresources.backup
cp -r resources/[qb]/qb-inventory resources/[qb]/qb-inventory.backup
cp -r resources/[qb]/qb-garages reso# Stop resources
stop qb-core
stop qb-smallresources
stop qb-inventory
stop qb-garages

# Restore from backup
rm -rf resources/[qb]/qb-core
rm -rf resources/[qb]/qb-smallresources
rm -rf resources/[qb]/qb-inventory
rm -rf resources/[qb]/qb-garages
cp -r resources/[qb]/qb-core.backup resources/[qb]/qb-core
cp -r resources/[qb]/qb-smallresources.backup resources/[qb]/qb-smallresources
cp -r resources/[qb]/qb-inventory.backup resources/[qb]/qb-inventory
cp -r resources/[qb]/qb-garages.backup resources/[qb]/qb-garages

# Restart resources
start qb-core
start qb-smallresources
start qb-inventory
start qb-garages-garages.backup
```

### 2. Environment Setup
- [ ] Test server prepared (separate from production)
- [ ] Multiple test accounts created
- [ ] Vehicle spawner available
- [ ] Admin permissions configured
- [ ] Performance monitoring tools ready

---

## Testing Procedures

### Phase 1: Core Functionality Tests

#### Test 1.1: Player Login/Logout
```
1. Login with test character
2. Check F8 console for errors
3. Verify player data loads correctly
4. Logout and verify clean disconnect
5. Check server console for save confirmations
```
**Expected Result:** No errors, smooth login/logout  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 1.2: Proximity Functions
```
1. Spawn multiple peds near player
2. Test /testclosestped (create if needed)
3. Verify correct closest ped detected
4. Repeat with vehicles and objects
5. Test in empty area (should return -1, -1)
```
**Expected Result:** Correct entity detection, no errors  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 1.3: Metadata Updates
```
1. Wait for hunger/thirst to decrease
2. Verify damage applies at 0 hunger/thirst
3. Check console for update events
4. Eat/drink to restore levels
```
**Expected Result:** Hunger/thirst decreases, damage applies correctly  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 2: Vehicle Mechanics Tests

#### Test 2.1: Seatbelt System
```
1. Enter vehicle
2. Press B to toggle seatbelt
3. Crash at moderate speed WITH seatbelt
4. Crash at high speed WITHOUT seatbelt
5. Verify ejection occurs correctly
```
**Expected Result:** Proper ejection mechanics, no errors  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 2.2: Cruise Control
```
1. Enter vehicle and accelerate
2. Press Y to activate cruise control
3. Verify speed maintenance
4. Test deactivation by:
   - Pressing Y again
   - Turning sharply
   - Applying handbrake
   - Taking damage
```
**Expected Result:** Smooth cruise activation/deactivation  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 2.3: Vehicle Push
```
1. Damage vehicle engine (below Config.DamageNeeded)
2. Exit vehicle
3. Use qb-target on bonnet/boot
4. Select "Push Vehicle"
5. Test steering (A/D keys)
6. Press E to stop pushing
```
**Expected Result:** Smooth pushing, responsive controls  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 3: AFK System Tests

#### Test 3.1: AFK Detection
```
1. Login and stay completely still
2. Wait for AFK warnings to appear
3. Move before kick threshold
4. Verify timer resets
5. Test actual AFK kick (if time permits)
```
**Expected Result:** Warnings appear, timer resets on movement  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 3.2: AFK Permissions
```
1. Test with admin account
2. Verify no AFK warnings appear (if admin exempt)
3. Test permission update on-the-fly
```
**Expected Result:** Permissions respected  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 4: Money Operations Tests

#### Test 4.1: Money Transactions
```
1. Use /givemoney cash 1000
2. Use /removemoney cash 500
3. Check console for log events
4. Verify balance updates in HUD
5. Test bank transactions
```
**Expected Result:** Transactions process correctly, logs created  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 5: Performance Tests

#### Test 5.1: Client Performance
```
1. Note baseline FPS in city center
2. Perform various actions for 10 minutes
3. Note FPS after optimization
4. Check for FPS drops or stutters
```
**Before FPS:** _______  
**After FPS:** _______  
**Improvement:** _______  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 5.2: Server Performance
```
1. Note server ms/tick in F8
2. Have multiple players perform actions
3. Monitor for 30+ minutes
4. Check for tick increases
```
**Before ms/tick:** _______  
**After ms/tick:** _______  
**Improvement:** _______  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 5.3: Memory Usage
```
1. Note resmon memory at startup
2. Play for 1 hour
3. Check memory usage
4. Look for memory leaks
```
**Resources to Monitor:**
- qb-core: Start: _______ After 1hr: _______
- qb-smallresources: Start: _______ After 1hr: _______

**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 6: Compatibility Tests

#### Test 6.1: QBCore Resources
```
Test the following resources for basic functionality:
- [ ] qb-inventory (open, use items)
- [ ] qb-target (proximity detection)
- [ ] qb-jobs (mechanic, police, etc.)
- [ ] qb-phone (calls, messages)
- [ ] qb-vehicleshop (purchase, test drive)
- [ ] qb-garages (store, retrieve)
- [ ] qb-banking (deposit, withdraw)
- [ ] qb-shops (purchase items)
```
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 6.2: Third-Party Resources
```
List and test any third-party resources using QBCore:
1. _________________ : ☐ Pass ☐ Fail
2. _________________ : ☐ Pass ☐ Fail
3. _________________ : ☐ Pass ☐ Fail
```
**Notes:** _________________

---

### Phase 7: Inventory & Garage Tests

#### Test 7.1: Inventory Operations
```
1. Add items to inventory (multiple types)
2. Remove items from inventory
3. Test full inventory scenarios
4. Open/close stashes and trunks
5. Check F8 for any errors
```
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 7.2: Dropped Item Cleanup
```
1. Drop several items on ground
2. Note the server time
3. Wait for Config.CleanupDropTime duration
4. Verify items are cleaned up automatically
5. Check server console for cleanup messages
```
**Cleanup Time:** _______ minutes  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 7.3: Garage Vehicle Retrieval
```
1. Test garage menu with no vehicles (should open instantly)
2. Test with 1-5 vehicles
3. Test with 10+ vehicles
4. Test category filtering (cars, boats, aircraft)
5. Test depot retrieval
```
**Performance:** ☐ Faster ☐ Same ☐ Slower  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 7.4: Slot Counting
```
1. Fill inventory to various levels (25%, 50%, 75%, 100%)
2. Check slot count accuracy (/inventory or similar)
3. Test with stashes
4. Test with vehicle trunks
5. Verify slot limits enforced correctly
```
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

### Phase 8: Stress Testing

#### Test 8.1: High Player Count
```
1. Have 10+ players online simultaneously
2. All players perform various actions
3. Monitor server performance
4. Check for any errors or crashes
```
**Player Count:** _______  
**Duration:** _______ minutes  
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

#### Test 8.2: Rapid Actions
```
1. Rapidly spawn/delete vehicles
2. Quick money transactions (100+ in succession)
3. Spam proximity checks
4. Monitor for errors or performance degradation
```
**Pass:** ☐ Yes ☐ No  
**Notes:** _________________

---

## Performance Metrics

### Client-Side Metrics
| Metric | Before | After | Change | Pass |
|--------|--------|-------|--------|------|
| FPS (City Center) | _____ | _____ | _____ | ☐ |
| FPS (Paleto Bay) | _____ | _____ | _____ | ☐ |
| Frame Time (ms) | _____ | _____ | _____ | ☐ |
| Memory (MB) | _____ | _____ | _____ | ☐ |

### Server-Side Metrics
| Metric | Before | After | Change | Pass |
|--------|--------|-------|--------|------|
| Server Tick (ms) | _____ | _____ | _____ | ☐ |
| CPU Usage (%) | _____ | _____ | _____ | ☐ |
| Memory (MB) | _____ | _____ | _____ | ☐ |
| Player Slots Used | _____ | _____ | _____ | ☐ |

---

## Error Logging

### Client Errors
```
Timestamp | Error Message | Severity | Resource
---------|---------------|----------|----------



```

### Server Errors
```
Timestamp | Error Message | Severity | Resource
---------|---------------|----------|----------



```

---

## Optimization Commands

### Useful Testing Commands
```lua
-- Create test command to check closest entities
RegisterCommand('testclosest', function()
    local ped = QBCore.Functions.GetClosestPed(GetEntityCoords(PlayerPedId()))
    local veh = QBCore.Functions.GetClosestVehicle(GetEntityCoords(PlayerPedId()))
    local obj = QBCore.Functions.GetClosestObject(GetEntityCoords(PlayerPedId()))
    print('Closest Ped:', ped)
    print('Closest Vehicle:', veh)
    print('Closest Object:', obj)
end)

-- Monitor player metadata
RegisterCommand('checkstatus', function()
    local metadata = QBCore.Functions.GetPlayerData().metadata
    print('Hunger:', metadata.hunger)
    print('Thirst:', metadata.thirst)
end)
```

---

## Decision Matrix

### Deploy to Production?

**All Critical Tests Passed:** ☐ Yes ☐ No  
**Performance Improvement Confirmed:** ☐ Yes ☐ No  
**No Breaking Bugs Found:** ☐ Yes ☐ No  
**Compatibility Verified:** ☐ Yes ☐ No  

**Final Decision:** ☐ DEPLOY ☐ ROLLBACK ☐ MORE TESTING NEEDED

**Deployment Date:** ______________  
**Deployed By:** ______________  

---

## Post-Deployment Monitoring

### First 24 Hours
- [ ] Check error logs every 2 hours
- [ ] Monitor player feedback
- [ ] Watch performance metrics
- [ ] Be ready to rollback if needed

### First Week
- [ ] Daily log review
- [ ] Gather player feedback
- [ ] Monitor long-term stability
- [ ] Document any issues

---

## Rollback Procedure

If rollback is needed:

```bash
# Stop affected resources
stop qb-core
stop qb-smallresources

# Restore from backup
rm -rf resources/[qb]/qb-core
rm -rf resources/[qb]/qb-smallresources
cp -r resources/[qb]/qb-core.backup resources/[qb]/qb-core
cp -r resources/[qb]/qb-smallresources.backup resources/[qb]/qb-smallresources

# Restart resources
start qb-core
start qb-smallresources
```

**Rollback Reason:** _________________  
**Rollback Date:** _________________  
**Rollback By:** _________________  

---

## Notes and Observations

### General Notes
```




```

### Recommendations
```




```

### Future Improvements
```




```

---

**Tester Name:** ______________  
**Test Date:** ______________  
**Test Duration:** ______________  
**Overall Result:** ☐ PASS ☐ FAIL ☐ CONDITIONAL PASS
