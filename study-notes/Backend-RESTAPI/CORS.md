Cross Origin Resource Sharing Error

logger.Critical(http.ListenAndServe(port, handlers.CORS(handlers.AllowedHeaders([]string{"*"}), handlers.AllowedMethods([]string{"*"}), handlers.AllowedOrigins([]string{"*"}))(router)))