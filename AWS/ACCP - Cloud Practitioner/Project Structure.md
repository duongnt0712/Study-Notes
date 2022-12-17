com.nt.rookies
     +- assets
         +- AssetManagementApplication.java
         |     
         +- config
         |   +-CorsConfig.java
         |   +-WebSecurityConfig.java
         |   
         +- controller
         |   +-UserController.java
         |   +-AssetController.java
         |   +-AssignmentController.java
         |   +-RequestReturnController.java
         |   +-AuthController.java
         |     
         +- dto
         |   +- UserDto.java
         |   +- AssetDto.java
         |   +- AssignmentDto.java
         |   +- ReturnRequestDto.java
         |   +- AuthorityDto.java
         |   +- CategoryDto.java
         |   +- LoginResponse.java
         |
         +- entity
         |   +- User.java
         |   +- Asset.java
         |   +- Assignment.java
         |   +- ReturningRequest.java
         |   +- Authority.java
         |   +- Category.java
         |
         +- exception
         |   +- BusinessException.java
         |   +- ErrorCode.java
         |   +- ExceptionHandlingController.java
         |
         +- repository
             +- impl [...]
         |   +- IUserRepository.java
         |   +- IAssetRepository.java
         |   +- IAssignmentRepository.java
         |   +- IReturningRequestRepository.java
         |   +- IAuthorityRepository.java
         |   +- ICategoryRepository.java
         |
         +- request
             +- baseEntity
             |  +- PagingBase.java
             |  +- SortBase.java
             |  +- DateBase.java
         |   +- LoginRequest.java
         |
         +- response
         |   +- ResponseData.java
         |   +- ResponseDataConfiguration.java
         |
         +- jwt
         |    +- JwtAuthenticationFilter.java
         |    +- JwtTokenProvider.java
         |    +- CustomUserDetails.java
         |
         +- services
             +- impl [...]
         |   +- IUserService.java
         |   +- IAssetService.java
         |   +- IAssignmentService.java
         |   +- IReturningRequestService.java
         |   +- IAuthorityService.java (?)
         |   +- ICategoryService.java (?)
         +- util [...]